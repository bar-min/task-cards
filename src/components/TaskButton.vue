<template>
  <button @click="$emit('show-cards')">Показать задачи</button>
</template>

<script>
export default {
  emits: ['show-cards']
}
</script>

<style>

</style>