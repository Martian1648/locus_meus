<script setup >
import {pl} from "vuetify/locale";

const toGo = [
  {
    title:"The Book of Concord",
    img: "Concordia.jpg",
    desc:"Read the Lutheran Confessions, those symbols that accurately" +
        " exposit the Christian faith according to the Scriptures, and thus" +
        " set the borders of orthodoxy.",
    link:"/",
    position: "center 7%"
  },
  {
    title:"Translated Works",
    img: "Jerome.jpg",
    desc:"The Lutheran dogmatic tradition is filled with valuable works, " +
        "some of which have been translated (professionally or otherwise) into" +
        " english.",
    link:"/",
    position: "center 20%"
  },
  {
    title:"Untranslated Works",
    img: "Templum.jpg",
    desc:"Many important works from our theologians are still found only in Latin or German, nevertheless " +
        "they can be valuable to look at for those who can read those languages.",
    link:"/",
    position: "center 7%"
  }
]
</script>

<template>
  <v-defaults-provider :defaults="{ VBtn: { variant: 'outlined', color: '#eee' } }">
<v-carousel
direction="vertical"
class="h-screen"
vertical-arrows="right"
hide-delimiters
crossfade=true
next-icon="mdi-menu-right"
prev-icon="mdi-menu-left">
  <v-carousel-item v-for="place in toGo" :key="place.title"
  :src="place.img" cover :position="place.position">
    <div class="d-flex-inline fill-height justify-center align-center
     text-white pa-10" style="background-color:rgba(38, 50, 56, .9); " >
      <h1 class="text-display-large text-center">
        {{place.title}}
      </h1>
      <v-divider></v-divider>
      <div class="pa-5">
        <v-container>
          <v-row>
            <v-col>{{place.desc}}</v-col>
            <v-col>
            <v-chip variant="outlined" link ripple=false append-icon="mdi-arrow-top-right">
              Go to {{place.title}}
            </v-chip></v-col>
          </v-row>
        </v-container></div>
    </div>
  </v-carousel-item>

</v-carousel>
  </v-defaults-provider>
</template>

<style scoped>

</style>