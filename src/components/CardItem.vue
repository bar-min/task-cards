<template>
  <div class="card">
    <h3 class="card__title">{{ task.title }}</h3>
    <p class="card__time"></p>
    <p class="card__category">Категория: {{ task.category }}</p>
    <div class="card__price">{{ task.price }} руб.</div>
  </div>
</template>

<script>
export default {
  props: ['task']
}
</script>

<style>

</style>