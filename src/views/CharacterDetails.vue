<script setup>
import { ref, onMounted } from 'vue';
import { useRoute } from 'vue-router';
import ky from 'ky';

const route = useRoute();
const characterDetails = ref(null);
const characterId = route.params.id;

const fetchCharacterDetails = async () => {
    try {
        const response = await ky.get(`https://www.amiiboapi.com/api/amiibo/?tail=${characterId}`).json();
        characterDetails.value = response.amiibo[0];
    } catch (error) {
        console.error('Error fetching character details:', error);
    }
};

onMounted(() => {
    fetchCharacterDetails();
});
</script>

<template>
    <section id="main">
        <div class="container">
            <div class="row">
                <div class="col-4 col-12-medium">

                    <!-- Sidebar -->
                    <section class="box" v-if="characterDetails">
                        <header>
                            <h3>Infos</h3>
                        </header>
                        <p>
                            amiiboSeries: <b>{{ characterDetails.amiiboSeries }}</b><br />
                            character: {{ characterDetails.character }}<br />
                            gameSeries: {{ characterDetails.gameSeries }}<br />
                            type: {{ characterDetails.type }}
                        </p>
                    </section>
                    <section class="box" v-if="characterDetails">
                        <header>
                            <h3>Dates sorties</h3>
                        </header>
                        <ul class="divided">
                            <li v-if="characterDetails.release.au">au: {{ characterDetails.release.au }}</li>
                            <li v-if="characterDetails.release.eu">eu: {{ characterDetails.release.eu }}</li>
                            <li v-if="characterDetails.release.jp">jp: {{ characterDetails.release.jp }}</li>
                            <li v-if="characterDetails.release.na">na: {{ characterDetails.release.na }}</li>
                        </ul>
                    </section>

                </div>
                <div class="col-8 col-12-medium imp-medium">

                    <!-- Content -->
                    <article class="box post" v-if="characterDetails">
                        <a href="#" class="featured">
                            <img :src="characterDetails.image" :alt="characterDetails.character" />
                        </a>
                        <header>
                            <h2>{{ characterDetails.name }}</h2>
                            <p>{{ characterDetails.type }}</p>
                        </header>
                    </article>
                </div>
            </div>
        </div>
    </section>
</template>

<style scoped>
</style>