<template>
  <div class="menu">
    <div class="menu__wrapper">
      <h2 class="menu__heading">Добавление задачи</h2>
      
      <div class="menu__title menu-required">
        <label for="title" class="label-menu">Наименование задачи</label>
        <input v-model='title' class='input-menu' id="title" maxlength="35" placeholder="Введите наименование">
      </div>

      <div class="menu__category">
        <label for="category" class="label-menu">Категория задачи</label>
        <select class="input-menu select" ref="select">
          <option v-for="(item, index) in categories" :key="index" :value='item' :selected="!index">
          {{ item }}
          </option>
        </select>
      </div>

      <div class="date">
        <div class="date__wrapper">
          <label for="start">Дата начала</label>
          <div class="date__start" id="start">
            <input type="date" v-model="start.date">
            <input type="time" v-model="start.time">
          </div>
        </div>

        <div class="date__wrapper">
          <label for="end">Дата окончания</label>
          <div class="date__end" id="end">
            <input type="date" v-model="end.date">
            <input type="time" v-model="end.time">
          </div>
        </div>
      </div>

      <div class="menu__price menu-required">
        <label for="price" class="label-menu">Цена задачи</label>
        <input v-model="price" class='input-menu' id="price" maxlength="8" placeholder="Введите цену">
      </div>
      <button @click="setTask" class="menu__btn">Добавить</button>
    </div>
  </div>
</template>

<script>
export default {
  props: ['categories'],
  emits: ['add-task'],

  data(){
    return {
      title: '',
      price: '',
      start: {
        date: '2022-08-15',
        time: '08:00'
      },
      end: {
        date: '2022-08-18',
        time: '16:00'
      }
    }
  },

  methods: {
    setTask(){
      const newTask = {
        title: this.title,
        category: this.$refs.select.value,
        price: this.price, 
        dateBegin: this.start.date + 'T' + this.start.time,
        dateEnd: this.end.date + 'T' + this.end.time,
      }
      this.$emit('add-task', newTask)
    }
  },

}
</script>

<style>

</style>