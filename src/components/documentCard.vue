<script setup>
import { ref, computed, onMounted } from 'vue';
import {getUser} from "../misc.js"
const props = defineProps({
  id:{type:Number, required:true},
  title:{type:String, required:true},
  short_title:{type:String, required:true},
  year_published:{type:Number, required:false},
  language:{type:String, required:true},
  author_id:{type:Number, required:true},
  author_name:{type:String, required:true},
  link:{type:String, required:true},
})

const user = ref(getUser());
const loading = ref(false);
const error = ref('');
const isLoggedIn = ref(false);
const snackbar=ref(false);
const message = ref("");
onMounted(() => {
  if(user.value){
    isLoggedIn.value = true;
  }
});



function open(link){
  window.open(link, "_blank")
}

async function checkOut(event) {
  event.stopPropagation();
  loading.value = true;
  error.value = '';

  try {
    const response = await fetch('/api/checked_outs', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({
        user_id: user.value.id,
        document_id: props.id,
      }),
    });

    const data = await response.json();

    if(response.status === 409){

      message.value=data.error;
      snackbar.value = true;
    }
    else if (response.status === 201){
      snackbar.value = false;
      message.value = "Book added to Library!";
      snackbar.value = true;
    }
    if (!response.ok) {
      throw new Error('Failed to check out');
    }



  } catch (error) {
    error.value = "Something went wrong";
  } finally {

    loading.value = false;
  }
}

</script>

<template>
  <v-defaults-provider :defaults="{VIcon:{color:'green-darken-3'}}">
<v-card link  @click="open(link)" append-icon="mdi-arrow-top-right">
  <v-card-title class="headline text-wrap">{{title}}</v-card-title>
  <v-card-subtitle>By {{author_name}} | Published: {{year_published}}</v-card-subtitle>
  <v-card-text>Language: {{language}}</v-card-text>
  <v-card-actions>
    <v-btn @click="checkOut($event)" :disabled="!isLoggedIn || loading"
    variant="outlined" color="green-darken-3">Checkout</v-btn>
  </v-card-actions>
</v-card>
  </v-defaults-provider>

<v-snackbar v-model="snackbar" top>
  {{message}}
  <template v-slot:actions>
    <v-btn
        color="green-darken-3"
        variant="text"
        @click="snackbar = false"
    >
      Close
    </v-btn>
  </template>
</v-snackbar>
</template>