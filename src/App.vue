<script setup>
import {ref, computed} from 'vue';
import home from './components/home.vue'
import about from './components/about.vue'

const routes = {
  '/': home,
  '/about': about,
}
const currentPath = ref(window.location.hash)

window.addEventListener('hashchange', e => {
  currentPath.value = window.location.hash;
})

const currentView = computed(() => {
  return routes[currentPath.value.slice(1) || '/'] || NotFound
})
</script>

<template>
  <nav>
    <a href="#/">Home</a>
    <a href="#/about">About</a>
  </nav>
  <h1>Locus Meus</h1>

  <component :is="currentView" />
</template>

<style scoped>

</style>
