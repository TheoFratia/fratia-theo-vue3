<script setup>
import { defineProps } from 'vue';
import { useRouter } from 'vue-router';

const props = defineProps({
  characters: Array,
});

const router = useRouter();

const viewDetails = (id) => {
  router.push({ name: 'CharacterDetails', params: { id } });
};
</script>

<template>
  <table>
    <thead>
      <tr>
        <th>Character</th>
        <th>Game Series</th>
        <th>Action</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(character, index) in characters" :key="index">
        <td>{{ character.character }}</td>
        <td>{{ character.gameSeries }}</td>
        <td><button @click="viewDetails(character.tail)">voir</button></td>
      </tr>
    </tbody>
  </table>
</template>

<style scoped>
</style>