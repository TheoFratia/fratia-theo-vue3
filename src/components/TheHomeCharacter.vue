<script setup>
defineProps({
  image: String,
  character: String,
  gameSeries: String,
});
</script>

<template>
  <div class="col-4 col-12-medium">
    <section class="middle">
      <img :src="image" alt="character image" />
      <header>
        <h2>{{ character }}</h2>
      </header>
      <p>{{ gameSeries }}</p>
    </section>
  </div>
</template>

<style scoped>
</style>