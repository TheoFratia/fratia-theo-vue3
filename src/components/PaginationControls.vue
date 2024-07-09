<script setup>
import { defineProps, defineEmits } from 'vue';

const props = defineProps({
  currentCount: Number,
  totalCount: Number,
});

const emit = defineEmits(['loadMore']);

const loadMore = () => {
  emit('loadMore');
};
</script>

<template>
  <div class="pagination">
    <p>Affichage de {{ currentCount }} sur {{ totalCount }}</p>
    <button @click="loadMore">Charger plus</button>
  </div>
</template>

<style scoped>
</style>