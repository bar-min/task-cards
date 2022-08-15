<template>
  <div class="card">
    <h3 class="card__title">{{ validTitle(task.title) }}</h3>
    <div class="card__date">Дата начала: {{ validDate(task.dateBegin) }}</div>
    <div class="card__date">Дата окончания: {{ validDate(task.dateEnd) }}</div>
    <p class="card__category">Категория: {{ task.category }}</p>
    <div class="card__price">{{ task.price }} руб.</div>
  </div>
</template>

<script>
export default {
  props: ['task'],

  methods: {
    validDate(date){
      if(date){
        let options = { year: 'numeric', month: 'long', day: 'numeric', hour: "numeric", minute: "numeric"} 
        return new Date(date).toLocaleDateString("ru-RU", options)
      } 
      return 'договорная'
    },
    validTitle(title){
      return title[0].toUpperCase() + title.slice(1).toLowerCase()
    }
  }
}
</script>

<style>

</style>