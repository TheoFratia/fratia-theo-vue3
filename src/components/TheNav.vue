<script setup>
import { useRoute } from 'vue-router';

const route = useRoute();
</script>

<template>
    <section id="header">
        <h1 v-if="route.path === '/'">AmiiVue</h1>
        <h1 v-else>Liste Amiibo</h1>
        <nav id="nav">
            <ul>
                <li :class="{ current: route.path === '/' }"><a href="/">Home</a></li>
                <li :class="{ current: route.path === '/list' }"><a href="/list">Liste Amiibo</a></li>
            </ul>
        </nav>
        <section v-if="route.path === '/'" id="banner">
            <header>
                <h2>Hey. Bienvenue sur ma collection</h2>
            </header>
        </section>
    </section>
</template>