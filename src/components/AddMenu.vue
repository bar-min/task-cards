<template>
  <transition name="menu">
    <div class="menu" v-if="menu">
      <div class="close" @click="$emit('close-menu')"></div>

      <div class="menu__wrapper">
        <h2 class="menu__heading">Добавление задачи</h2>
        
        <div class="menu__title" :class="{'menu-required': !isValidTitle}">
          <label for="title" class="label-menu">Наименование задачи</label>
          <input v-model='title' @blur="checkInput" class='input-menu' id="title" maxlength="35" placeholder="Введите наименование">
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
          <div class="date__wrapper" :class="{'menu-required': !validDate}">
            <label for="start">Дата начала</label>
            <div class="date__start" id="start">
              <input type="date" :value="start.date" @input="checkDate($event, 'start')">
              <input type="time" v-model="start.time">
            </div>
          </div>

          <div class="date__wrapper" :class="{'menu-required': !validDate}">
            <label for="end">Дата окончания</label>
            <div class="date__end" id="end">
              <input type="date" :value="end.date" @input="checkDate($event, 'end')">
              <input type="time" v-model="end.time">
            </div>
          </div>
        </div>

        <div class="menu__price" :class="{'menu-required': !isValidPrice}">
          <label for="price" class="label-menu">Цена задачи</label>
          <input :value="price" @input="checkPrice" @blur="checkInput" class='input-menu' id="price" maxlength="8" placeholder="Введите цену">
        </div>

        <button @click="setTask" 
        class="menu__btn" 
        :class="{'menu__btn_active': isValid}"  
        :disabled="!isValid">Добавить</button>

      </div>
    </div>
  </transition>
</template>

<script>
export default {
  props: ['categories', 'menu'],
  emits: ['add-task', 'close-menu'],

  data(){
    return {
      title: '',
      price: '',
      start: {
        date: '2022-08-15',
        time: '08:00',
      },
      end: {
        date: '2022-08-18',
        time: '16:00'
      },
      isValidTitle: true,
      isValidPrice: true,
    }
  },

  computed: {
    isValid(){
      return (this.title && this.price && this.validDate) ? true : false
    },
    validPrice(){
      return +this.price.replace(/\s/g, "")
    },
    validDate(){
      return this.modifyDate(this.dateStart) < this.modifyDate(this.dateEnd) ? true : false
    },
    dateStart(){
      return this.start.date + '\n' + this.start.time
    },
    dateEnd(){
      return this.end.date + '\n' + this.end.time
    }
  },

  methods: {
    setTask(){
      const newTask = {
        title: this.title,
        category: this.$refs.select.value,
        price: this.validPrice, 
        dateBegin: this.dateStart,
        dateEnd: this.dateEnd,
        id: Date.now()
      }
      this.$emit('add-task', newTask)

      this.clearInputs();
    },

    checkInput(){
      this.isValidTitle = (!this.title) ? false : true; 
      this.isValidPrice = (!this.price) ? false : true; 
    },

    checkDate(event, type = 'start'){
      const inputDate = event.target.value;
      const max = this.modifyDate('2024-01-01');  
      const min = this.modifyDate('2022-01-01');
      let current = this.modifyDate(inputDate);

      if(max >= current && current >= min){
        this[type].date = inputDate;
      } else {
        event.target.value = this[type].date;
      }
    },

    modifyDate(date){
      return Date.parse(new Date(date));
    },

    checkPrice(event){
      const inputValue = event.target.value.replace(/\s/g, "");

      if(isNaN(inputValue)){
        event.target.value = this.price;
      } else {
        this.price = (+inputValue).toLocaleString();
      }
    },

    clearInputs(){
      this.title = '';
      this.price = '';
    }
  },

}
</script>

<style>

</style>