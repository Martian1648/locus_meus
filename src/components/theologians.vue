<script setup>
import TheologianCard from "@/components/theologianCard.vue";

const theologians = [
  {
    "name":"Martin Luther",
    "birth":"1483",
    "death":"1546",
    "location":"Wittenberg",
    "occupation":"Professor of Theology",
    "link":"https://en.wikipedia.org/wiki/Martin_Luther",
    "image":"Luther.png"
  },
  {
    "name":"Philipp Melanchthon",
    "birth":"1497",
    "death":"1560",
    "location":"Wittenberg",
    "occupation":"Professor of Greek",
    "link":"https://en.wikipedia.org/wiki/Philipp_Melanchthon",
    "image":""
  },
  {
    "name":"Martin Chemnitz",
    "birth":"1522",
    "death":"1586",
    "location":"Braunschweig",
    "occupation":"Theologian and Superintendent",
    "link":"https://en.wikipedia.org/wiki/Martin_Chemnitz",
    "image":""
  },
  {
    "name":"Johann Gerhard",
    "birth":"1582",
    "death":"1637",
    "location":"Jena",
    "occupation":"Professor of Theology",
    "link":"https://en.wikipedia.org/wiki/Johann_Gerhard",
    "image":""
  },
  {
    "name":"Aegidius Hunnius",
    "birth":"1550",
    "death":"1603",
    "location":"Wittenberg",
    "occupation":"Professor of Theology",
    "link":"https://en.wikipedia.org/wiki/Aegidius_Hunnius",
    "image":""
  },
  {
    "name":"Leonhard Hutter",
    "birth":"1563",
    "death":"1616",
    "location":"Wittenberg",
    "occupation":"Professor of Theology",
    "link":"https://en.wikipedia.org/wiki/Leonhard_Hutter",
    "image":""
  },
  {
    "name":"Abraham Calov",
    "birth":"1612",
    "death":"1686",
    "location":"Wittenberg",
    "occupation":"Professor of Theology",
    "link":"https://en.wikipedia.org/wiki/Abraham_Calovius",
    "image":""
  },
  {
    "name":"Johann Franz Buddeus",
    "birth":"1667",
    "death":"1729",
    "location":"Jena",
    "occupation":"Professor of Theology",
    "link":"https://en.wikipedia.org/wiki/Johann_Franz_Buddeus",
    "image":""
  },
  {
    "name":"Carl Ferdinand Wilhelm Walther",
    "birth":"1811",
    "death":"1887",
    "location":"St. Louis",
    "occupation":"Pastor and Theologian",
    "link":"https://en.wikipedia.org/wiki/C._F._W._Walther",
    "image":""
  }
]

function gotoWiki(link) {
  window.open(link, "_blank")
}
</script>

<template>
<v-container class="grid">
  <v-row>
    <v-col cols="4" v-for="theologian in theologians" :key="theologian.name">
    <TheologianCard
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

