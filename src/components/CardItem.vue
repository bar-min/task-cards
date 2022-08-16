<template>
  <div class="card">
    <h3 class="card__title">{{ setValidUnits(task.title, 'title') }}</h3>
    <div class="card__date">Дата начала: {{ setValidUnits(task.dateBegin, 'date') }}</div>
    <div class="card__date">Дата окончания: {{ setValidUnits(task.dateEnd, 'date') }}</div>
    <p class="card__category">Категория: {{ setValidUnits(task.category) }}</p>
    <div class="card__price">{{ setValidUnits(task.price, 'price') }}</div>
    <div class="card__remove" @click="$emit('del-task', task.id)"></div>
  </div>
</template>

<script>
export default {
  props: ['task'],
  emits: ['del-task'],

  methods: {
    setValidUnits(value, type = 'default', unit = 'руб.'){
      switch(type){
        case 'title': {
          return value[0].toUpperCase() + value.slice(1).toLowerCase()
        }
        case 'date': {
          if(value){
            let options = { year: 'numeric', month: 'long', day: 'numeric', hour: "numeric", minute: "numeric"} 
            return new Date(value).toLocaleDateString("ru-RU", options)
          }
          return 'договорная'
        }
        case 'price': {
          return value.toLocaleString() + '\n' + unit;
        }
        default: {
          return value.toLowerCase()
        }
      }
    },
  }
}
</script>

<style>

</style>