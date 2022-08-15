<template>
  <menu-button></menu-button>
  <task-button></task-button>

  <task-cards></task-cards>
</template>

<script>
import TaskCards from './components/TaskCards.vue';
import TaskButton from './components/TaskButton.vue';
import MenuButton from './components/MenuButton.vue';

export default {
  name: 'App',

  data(){
    return {
      cards: []
    }
  },

  methods: {
    async getTasksData(){
      try {
        const params = new URLSearchParams({ pagingCount: 10, pagingAfter: 0 })

        let response = await fetch(`http://api.staging.umeu.app/test/tasks/search?${params}`);

        let data = await response.json();
        
        this.setTasks(data);
      }
      catch(err){
        console.log(err)
      }
    },

    setTasks(data){
      let { result: { offers } } = data
      this.cards = offers;
    }
  },

  mounted(){
    this.getTasksData()

  },

  components: { TaskCards, TaskButton, MenuButton }
}
</script>

<style>
</style>
