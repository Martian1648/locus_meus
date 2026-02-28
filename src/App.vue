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

const navItems = [
  {
    title: 'Home',
    link: '#/',
    icon: 'mdi-home',
    show:false,
  },
  {
    title: 'About',
    link: '#/about',
    icon: 'mdi-information',
    show:false,
  }
]

const showItems = ref(false)
</script>

<template>
  <v-app>
<!--  <nav>-->
<!--    <a href="#/">Home</a>-->
<!--    <a href="#/about">About</a>-->
<!--  </nav>-->
<!--  <h1>Locus Meus</h1>-->
  <v-navigation-drawer permanent width="200"
                       @mouseenter="showItems = true"
  @mouseleave="showItems = false"
  color="green-darken-3" class="text-blue-grey-lighten-5">

    <v-list-item-title  class="text-center text-h6" >LuTheologus</v-list-item-title>

    <v-divider></v-divider>
    <div v-for="item in navItems" :key="item.title">
      <v-list-item link :href="item.link" >
        <v-row>
          <v-col>
        <v-icon >{{ item.icon }}</v-icon>
          </v-col>
          <v-col>
            <v-list-item-title v-if="showItems">{{ item.title }}</v-list-item-title>
          </v-col>
        </v-row>
      </v-list-item>
    </div>
  </v-navigation-drawer>

  <v-main>
    <component :is="currentView" />
  </v-main>
  </v-app>
</template>

<style scoped>

</style>
