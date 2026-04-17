<script setup>
import TheologianCard from "@/components/theologianCard.vue";
import {onMounted, ref} from 'vue';

const theologians = ref([])
const loading = ref(true)
const error = ref('')

async function loadTheologians() {
  loading.value = true;
  error.value = "";

  try {
    const response = await fetch("http://localhost:3000/authors")
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
  catch(error) {
    error.value = error.message || "Something went wrong";
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

