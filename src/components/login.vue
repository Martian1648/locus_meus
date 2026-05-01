<script setup>
import { ref } from 'vue';
const name = ref('');
const loading = ref(false);
const error = ref('');
const user = ref(null);


async function submit() {
  const trimmed = name.value.trim();
  if (!trimmed) {
    error.value = 'Please enter a name';
    return;
  }

  loading.value = true;
  error.value = '';

  try {

    const response = await fetch('/api/users', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({ name: trimmed }),
    });

    if (!response.ok) {
      throw new Error('Login failed');
    }

    const data = await response.json();
    user.value = data;
    localStorage.setItem('user', JSON.stringify(data));
    window.location.reload();
    window.location.hash = '/documents';

  } catch (err) {
    error.value =  'Something went wrong';
  } finally {
    loading.value = false;
  }
}

</script>

<template>

  <h1 class="bg-grey-darken-4 text-h2 text-center pa-3  mb-5">Log In or Create Account</h1>
  <v-form @submit.prevent="submit" class="w-75 ma-10">
    <v-text-field label="Username" required variant="underlined" color="green-darken-3" v-model="name" autofocus></v-text-field>

    <v-hover v-slot="{isHovering, props}">
      <v-btn type="submit"  color="green-darken-3"
             :variant="isHovering? 'elevated' : 'outlined'"
             :class="{'on-hover': isHovering}"
             v-bind="props">Submit</v-btn>
    </v-hover>
  </v-form>
</template>