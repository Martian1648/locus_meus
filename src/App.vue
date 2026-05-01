<script setup>
import {ref, computed, onMounted} from 'vue';
import home from './components/home.vue'
import about from './components/about.vue'
import theologians from "@/components/theologians.vue";
import documents from "@/components/documents.vue";
import login from "@/components/login.vue";
import library from "@/components/library.vue";
import {getUser} from "@/misc.js";

const routes = {
  '/': home,
  '/about': about,
  '/theologians': theologians,
  '/documents': documents,
  '/login': login,
  '/library': library,
}
const currentPath = ref(window.location.hash)

window.addEventListener('hashchange', e => {
  currentPath.value = window.location.hash;
})

const currentView = computed(() => {
  return routes[currentPath.value.slice(1) || '/']
})

const navItems = computed(() => {
  const items = [
    { title: 'Home', link: '#/', icon: 'mdi-home' },
    { title: 'About', link: '#/about', icon: 'mdi-information' },
    { title: 'Theologians', link: '#/theologians', icon: 'mdi-crowd' },
    { title: 'Documents', link: '#/documents', icon: 'mdi-file-document-multiple-outline' },
  ];
  if (isLoggedIn.value) {
    items.push({ title: 'Library', link: '#/library', icon: 'mdi-bookshelf' });
  } else {
    items.push({ title: 'Login', link: '#/login', icon: 'mdi-login' });
  }
  return items;
});

function logout(){
  isLoggedIn.value = false;
  localStorage.removeItem('user');
  window.location.reload();
}
const isLoggedIn = ref(false);
const user = ref(getUser());
onMounted(()=> {
  if(user.value){
    isLoggedIn.value = true;

  }
})
</script>

<template>
  <v-app theme="dark">
<!--  <nav>-->
<!--    <a href="#/">Home</a>-->
<!--    <a href="#/about">About</a>-->
<!--  </nav>-->
<!--  <h1>Locus Meus</h1>-->
  <v-navigation-drawer permanent width="200"

  color="green-darken-3" class="text-blue-grey-lighten-5">

    <v-list-item-title  class="text-center text-h6" >LuTheologus</v-list-item-title>

    <v-divider></v-divider>
    <div v-for="item in navItems" :key="item.title">
      <v-list-item link :href="item.link"  >
        <v-row>
          <v-col>
        <v-icon >{{ item.icon }}</v-icon>
          </v-col>
          <v-col>
            <v-list-item-title  >{{ item.title }}</v-list-item-title>
          </v-col>
        </v-row>
      </v-list-item>
    </div>
    <template #append>
      <div class="d-flex justify-center pa-4">
        <v-btn @click="logout" v-if="isLoggedIn" variant="outlined">
          Logout
        </v-btn>
      </div>
    </template>
  </v-navigation-drawer>

  <v-main>
    <component :is="currentView" />
  </v-main>
  </v-app>
</template>

<style scoped>

</style>