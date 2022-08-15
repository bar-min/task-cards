<template>
  <button @click="$emit('show-menu')">Показать меню</button>
</template>

<script>
export default {
  emits: ['show-menu']
}
</script>

<style>

</style>