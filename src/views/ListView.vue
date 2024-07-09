<script setup>
import { ref, onMounted } from 'vue';
import ky from 'ky';
import CharacterTable from '../components/CharacterTable.vue';
import PaginationControls from '../components/PaginationControls.vue';

const characters = ref([]);
const currentCount = ref(0);
const totalCount = ref(0);
const pageSize = 10;

const fetchCharacters = async () => {
  try {
    const response = await ky.get('https://www.amiiboapi.com/api/amiibo/').json();
    const allCharacters = response.amiibo;
    totalCount.value = allCharacters.length;
    characters.value = allCharacters.slice(0, currentCount.value + pageSize);
    currentCount.value += pageSize;
  } catch (error) {
    console.error('Error fetching data:', error);
  }
};

const loadMore = () => {
  if (currentCount.value < totalCount.value) {
    fetchCharacters();
  }
};

onMounted(() => {
  fetchCharacters();
});
</script>

<template>
  <div id="page-wrapper">
    <!-- Main -->
    <section id="main">
      <div class="container">
        <!-- Content -->
        <article class="box post">
          <header>
            <h2>Ma Collection ({{ currentCount }} par {{ totalCount }})</h2>
          </header>
          <CharacterTable :characters="characters" />
          <PaginationControls
            :currentCount="currentCount"
            :totalCount="totalCount"
            @loadMore="loadMore"
          />
        </article>
      </div>
    </section>

    <!-- Footer -->
    <section id="footer">
      <div class="container">
        <div class="row">
          <div class="col-12">
            <!-- Copyright -->
            <div id="copyright">
              <ul class="links">
                <li>&copy;AmiiVue ~ 2024 </li>
                <li>Design: <a href="http://html5up.net">HTML5 UP</a></li>
              </ul>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<style scoped>
</style>