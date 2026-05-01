<script setup>
import TheologianCard from "@/components/theologianCard.vue";
import {onMounted, ref} from 'vue';
const real = "/api/authors"
const test = "http://localhost:3000"
const theologians = ref([])
const loading = ref(true)
const error = ref('')

async function loadTheologians() {
  loading.value = true;
  error.value = "";

  try {
    const response = await fetch("/api/authors")
    if(!response.ok) {
      throw new Error('failed to load authors')
    }

    const data = await response.json();
    theologians.value = data.map((theo) =>({
      id: theo.id,
      name: theo.name,
      birth: theo.birth,
      death: theo.death,
      location: theo.location,
      occupation: theo.occupation,
      link: theo.link,
      image: theo.image,
    }))
  }
  catch(err) {
    error.value = "Something went wrong";
  }
  finally {
    loading.value = false;
  }

}
function gotoWiki(link) {
  window.open(link, "_blank")
}
onMounted(() => {loadTheologians()})
</script>

<template>
  <h1 class="bg-grey-darken-4 text-h2 text-center pa-3">Authors</h1>
  <v-alert
      v-if="error"
      type="error"
      variant="tonal"
      class="mb-4"
  >
    {{ error }}
  </v-alert>
<v-container class="grid">
  <v-row>
    <v-col cols="4" v-for="theologian in theologians" :key="theologian.name">
    <TheologianCard
        :id="theologian.id"
      :name="theologian.name"
      :birth="theologian.birth"
      :death="theologian.death"
      :location="theologian.location"
      :occupation="theologian.occupation"
      :image="theologian.image"
      :link="theologian.link"
    @goto-wiki="gotoWiki(theologian.link)"/>
    </v-col>
  </v-row>
</v-container>
</template>