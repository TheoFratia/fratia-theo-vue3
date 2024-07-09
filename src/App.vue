<script setup>
import { RouterLink, RouterView } from 'vue-router'
import Nav from './components/TheNav.vue'
import Footer from './components/TheFooter.vue'
</script>

<template>
  <Nav />
  <main>
    <router-view></router-view>
  </main>
  <Footer />
</template>

<style scoped>
</style>
