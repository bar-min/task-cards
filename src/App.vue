<template>
  <main class="blocks">
    <div class="blocks__container blocks-wrapper">
      <add-menu :menu="menu" :categories="categories" @add-task="addTask"></add-menu>

      <div class="blocks__buttons">
        <task-button @show-cards="showCards">Показать задачи</task-button>
        <task-button @show-menu="showMenu">Показать меню</task-button>
      </div>

      <div class="blocks__cards">
        <task-cards :show="show" :cards="cards" @remove-task="deleteTask"></task-cards>
      </div>
    </div>
  </main>
</template>

<script>
import TaskCards from './components/TaskCards.vue';
import TaskButton from './components/TaskButton.vue';
import AddMenu from './components/AddMenu.vue'

export default {
  name: 'App',

  data(){
    return {
      cards: [],
      categories: [],
      show: false,
      menu: false
    }
  },

  methods: {
    async getTasksData(){
      try {
        const params = new URLSearchParams({ pagingCount: 9, pagingAfter: 0 })

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
      this.categories = Array.from(new Set(this.cards.map(item => item.category)));
    },
    addTask(task){
      this.cards.push(task)
    },
    deleteTask(id){
      let idx = this.cards.findIndex(item => item.id === id);
      this.cards.splice(idx, 1);
    },
    showCards(){
      this.show = !this.show;
    },
    showMenu(){
      this.menu = !this.menu;
    }
  },

  mounted(){
    this.getTasksData()
  },

  components: { TaskCards, TaskButton, AddMenu }
}
</script>

<style>
</style>
