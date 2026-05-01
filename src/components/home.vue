<script setup >

const toGo = [
  {
    title:"The Book of Concord",
    img: "Concordia.jpg",
    desc:"Read the Lutheran Confessions, those symbols that accurately" +
        " exposit the Christian faith according to the Scriptures, and thus" +
        " set the borders of orthodoxy.",
    link:"https://bookofconcord.org/",
    position: "center 7%"
  },
  {
    title:"Documents",
    img: "Jerome.jpg",
    desc:"These are all the documents, translated or otherwise, available to be read.",
    link:"#/documents",
    position: "center 20%"
  },
  {
    title:"Your Library",
    img: "Templum.jpg",
    desc:"These are the books you have set aside",
    link:"#/library",
    position: "center 7%"
  }
]

function openLink(link, internal) {
  if (internal) {
    window.location.hash = link;
  }
  else{
    window.open(link, "_blank")
  }
}
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
            <v-chip variant="outlined" link ripple=false append-icon="mdi-arrow-top-right"
            @click="openLink(place.link, false)">
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