<template>
  <div class="cards">
    <card-item v-for="card in cards" :key="card.id" :task="card"></card-item>
  </div>
</template>

<script>
import CardItem from './CardItem.vue';

export default {
  props: ['cards'],

  components: { CardItem }
}
</script>

<style>

</style>