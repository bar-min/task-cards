<template>
  <transition-group class="cards" name="list" tag="div" v-if="show" appear>
    <card-item v-for="card in cards" :key="card.id" :task="card" @del-task="removeTask"></card-item>
  </transition-group>
</template>

<script>
import CardItem from './CardItem.vue';

export default {
  props: ['cards', 'show'],
  emits: ['remove-task'],

  methods: {
    removeTask(id){
      this.$emit('remove-task', id)
    }
  },

  components: { CardItem }
}
</script>

<style>

</style>