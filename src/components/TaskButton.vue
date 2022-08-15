<template>
  <button @click="$emit('show-cards'), $emit('show-menu')"><slot></slot></button>
</template>

<script>
export default {
  emits: ['show-cards', 'show-menu']
}
</script>

<style>

</style>