<script setup>
const imageHeight = 2277
const sliceHeight = imageHeight / 4

const panels = [
  {
    title: 'What is the point (of this site)?',
    text: 'To provide a convenient hub for the common folk to read their favorite Lutheran theologians',
  },
  {
    title: 'Why?',
    text: 'Mostly because I want to pass my class',
  },
  {
    title: 'Who brought this site into being?',
    text: 'Remotely, God, as he is the first mover of all things. However, proximately, that would be me, myself, & I',
  },
  {
    title: 'About the creator',
    text: 'I am absolutely not putting that on the world wide web.',
  },
]
</script>

<template>
  <h1 class="bg-grey-darken-4 text-h2 text-center pa-3">About</h1>

  <v-expansion-panels variant="accordion" class="bg-grey-darken-4" flat tile>
    <v-expansion-panel
        v-for="(panel, index) in panels"
        :key="panel.title"
        class="bg-grey-darken-4"
        hide-actions
    >
      <template #title>
        <div
            class="image-slice"
            :style="{
            height: `${sliceHeight}px`,
            backgroundPositionY: `-${index * sliceHeight}px`
          }"
        >
          <div class="text-center text-h2 font-weight-bold">
            {{ panel.title }}
          </div>
        </div>
      </template>

      <template #text>
        <v-sheet color="grey-darken-3" class="pa-4">
          {{ panel.text }}
        </v-sheet>
      </template>
    </v-expansion-panel>
  </v-expansion-panels>
</template>

<style scoped>
/*I did use the help of AI for some of this styling*/
.image-slice {
  width: 100%;
  background-image:
      linear-gradient(rgba(0, 0, 0, 0.35), rgba(0, 0, 0, 0.35)),
      url("/Schmidt.jpg");
  background-repeat: no-repeat;
  background-position-x: center;
  background-size: auto 2277px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
}

:deep(.v-expansion-panel) {
  margin-top: 0 !important;
}

:deep(.v-expansion-panel::after) {
  display: none;
}

:deep(.v-expansion-panel-title) {
  padding: 0 !important;
  min-height: unset !important;
}

:deep(.v-expansion-panel-title__overlay) {
  display: none;
}
</style>