<template>
  <main class="blocks">
    <div class="blocks__container blocks-wrapper">
      <add-menu :menu="menu" :categories="categories" @add-task="addCard" @close-menu="showMenu"></add-menu>

      <div class="blocks__buttons">
        <show-button @show-cards="showCards">Показать задачи</show-button>
        <show-button @show-menu="showMenu">Показать меню</show-button>
      </div>

      <div class="blocks__cards">
        <task-cards :show="show" :cards="cards" @remove-task="deleteCard"></task-cards>
      </div>
    </div>
  </main>
</template>

<script>
import TaskCards from './components/TaskCards.vue';
import ShowButton from './components/ShowButton.vue';
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
    async getTasksFromAPI(){
      try {
        const params = new URLSearchParams({ pagingCount: 9, pagingAfter: 0 })

        let response = await fetch(`http://api.staging.umeu.app/test/tasks/search?${params}`);

        let data = await response.json();
        
        this.setCards(data);
      }
      catch(err){
        console.log(err)
      }
    },
    setCards(data){
      let { result: { offers } } = data
      this.cards = offers;
      this.categories = Array.from(new Set(this.cards.map(item => item.category)));
    },
    addCard(task){
      this.cards.push(task)
    },
    deleteCard(id){
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
    this.getTasksFromAPI()
  },

  components: { TaskCards, ShowButton, AddMenu }
}
</script>

<style>
</style>
