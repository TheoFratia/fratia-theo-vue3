<script setup>
import { ref, onMounted } from 'vue';
import ky from 'ky';
import homeCharacter from '../components/TheHomeCharacter.vue';

const characters = ref([]);

onMounted(async () => {
  try {
    const response = await ky.get('https://www.amiiboapi.com/api/amiibo/').json();
    characters.value = response.amiibo.slice(0, 3);
  } catch (error) {
    console.error('Error fetching data:', error);
  }
});
</script>

<template>
  <main>
    <section id="intro" class="container">
      <div class="row">
        <homeCharacter
          v-for="(character, index) in characters"
          :key="index"
          :image="character.image"
          :character="character.character"
          :gameSeries="character.gameSeries"
        />
      </div>
      <footer>
        <ul class="actions">
          <li><a href="/list" class="button large">Liste complète</a></li>
        </ul>
      </footer>
    </section>
  </main>
</template>