<script setup lang="ts">
</script>

<template>
  <h1 class="bg-grey-darken-4 text-h1 text-center">De Hoc Sito</h1>
  <v-expansion-panels variant="accordion" class="bg-grey-darken-4">

    <v-expansion-panel class="bg-grey-darken-4" hide-actions>
      <template #title>
        <v-img
            src="Schmidt.jpg"
            height="325.128"
            position="center 0%"
            cover
            class="d-flex align-center px-4 text-white"
            image-class="darken"
        >

          <div class="text-center text-h2 font-weight-bold">Propter quid?</div>
        </v-img>
      </template>

      <template #text>
        <v-sheet color="grey-darken-3" class="pa-4">
          The proximate external final cause (id est the "propter quid") is that I am doing this for a class.
        </v-sheet>
      </template>
    </v-expansion-panel>


    <v-expansion-panel  class="bg-grey-darken-4" hide-actions>
      <template #title>
        <v-img
            src="Schmidt.jpg"
            height="325.128"
            position="center 33%"
            cover
            class="d-flex align-center   text-white "
        >
          <div class="text-center text-h2 font-weight-bold">Cur?</div>
        </v-img>
      </template>

      <template #text>
        <v-sheet color="grey-darken-3" class="pa-4 ">
          The proximate internal final cause (id est the "cur") is that I have an enormous love for theology and for the works that have been translated, and I wanted them to be shown.
        </v-sheet>
      </template>
    </v-expansion-panel>


    <v-expansion-panel class="bg-grey-darken-4" hide-actions>
      <template #title>
        <v-img
            src="Schmidt.jpg"
            height="325.128"
            position="center 66%"
            cover
            class="d-flex align-center px-4 text-white"
        >
          <div class="text-center text-h2 font-weight-bold">Quae est causa efficiens?</div>
        </v-img>
      </template>

      <template #text>
        <v-sheet color="grey-darken-3" class="pa-4">
          Remotely, God, as he is the first mover of all things. However, proximately, the efficient cause is me, myself, & I
        </v-sheet>
      </template>
    </v-expansion-panel>


    <v-expansion-panel class="bg-grey-darken-4" hide-actions>
      <template #title>
        <v-img
            src="Schmidt.jpg"
            height="325.128"
            width="fit-content"
            position="center 100%"
            cover
            class="d-flex align-center px-4 text-white"
        >
          <div class="text-center text-h2 font-weight-bold">De me</div>
        </v-img>
      </template>

      <template #text>
        <v-sheet color="grey-darken-3" class="pa-4">
          I am absolutely not putting that on the world wide web.
        </v-sheet>
      </template>
    </v-expansion-panel>

  </v-expansion-panels>

</template>



