<template>
  <main class="blocks">
    <div class="blocks__container blocks-wrapper">
      <div class="blocks__buttons">
        <task-button @show-cards="showCards"></task-button>
        <menu-button></menu-button>
      </div>

      <div class="blocks__cards">
        <task-cards :cards="cards" v-if="show"></task-cards>
      </div>
    </div>
  </main>
</template>

<script>
import TaskCards from './components/TaskCards.vue';
import TaskButton from './components/TaskButton.vue';
import MenuButton from './components/MenuButton.vue';

export default {
  name: 'App',

  data(){
    return {
      cards: [],
      show: false
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
    },

    showCards(){
      this.show = !this.show;
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
