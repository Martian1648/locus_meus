<script setup>
const props =defineProps({
  id:{type: Number, required: true},
  name:{type:String,required: true},
  birth:{type:String,required: true},
  death:{type:String,required: true},
  location:{type:String,required: true},
  occupation:{type:String,required: false},
  link:{type:String,required: false},
  image:{type:String,required: false},
})
const emit = defineEmits(['goto-wiki'])
</script>

<template>

<v-card hover class="w-full" link  @click="emit('goto-wiki')" append-icon="mdi-arrow-top-right"
>






<v-card-title class="text-wrap" >{{name}}
 </v-card-title>
  <v-card-subtitle class="text-wrap">{{occupation}}, {{location}}</v-card-subtitle>
  <v-card-text> <v-list-item class="" prepend-icon="mdi-cake-variant">{{birth}}</v-list-item>
    <v-list-item  prepend-icon="mdi-grave-stone">{{death}}</v-list-item></v-card-text>
  <v-tooltip activator="parent" location="end">To {{name}}'s Wikipedia page</v-tooltip>

</v-card>


</template>


