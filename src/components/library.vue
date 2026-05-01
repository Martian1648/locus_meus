<script setup>
import { ref, onMounted } from 'vue';
import {getUser} from "@/misc.js";

const checkedOuts = ref([]);
const loading = ref(true);
const error = ref('');
const user = ref(getUser());
const bookmarkDialog = ref(false);
const bookmarkTarget = ref(null);
const bookmarkInput = ref(0);


onMounted(() => {
  if (user.value) {
    loadCheckedOuts();
  } else {
    loading.value = false;
    window.location.hash = '/';
  }
});

async function loadCheckedOuts() {
  loading.value = true;
  error.value = '';
  try {
    const response = await fetch(`/api/checked_outs/user/${user.value.id}`);
    if (!response.ok) {
      throw new Error('Failed to load checked outs');
    }
    checkedOuts.value = await response.json();
  } catch (err) {
    error.value = 'Something went wrong';
  } finally {
    loading.value = false;
  }
}

async function setLastOpened(item){
  error.value = '';
  try {
    const response = await fetch(`/api/checked_outs/${item.id}/last_opened`, {
      method:'POST',
    })
    if (!response.ok) {
      throw new Error('Failed to update last_opened');
    }
    const updated = await response.json();
    const idx = checkedOuts.value.findIndex((c) => c.id === updated.id);
    if (idx !== -1) {
      checkedOuts.value[idx].last_opened = updated.last_opened;
    }
  }
  catch(err) {
    error.value = 'Something went wrong';
  }
  finally {
  }
}

async function openDocument(item) {
  window.open(item.link, '_blank');
   setLastOpened(item);

}

async function removeCheckout(item, event) {
  event.stopPropagation();
  try {
    const response = await fetch(`/api/checked_outs/${item.id}`, {
      method: 'DELETE',
    });
    if (!response.ok) {
      throw new Error('Failed to remove');
    }
    checkedOuts.value = checkedOuts.value.filter((c) => c.id !== item.id);
  } catch (err) {
    error.value = 'Something went wrong';
  }
}

function openBookmarkDialog(item, event) {
  event.stopPropagation();
  bookmarkTarget.value = item;
  bookmarkInput.value = item.bookmark_page;
  bookmarkDialog.value = true;
}

async function saveBookmark() {
  try {
    const response = await fetch(
        `/api/checked_outs/${bookmarkTarget.value.id}/bookmark`,
        {
          method: 'POST',
          headers: { 'Content-Type': 'application/json' },
          body: JSON.stringify({ bookmark_page: Number(bookmarkInput.value) }),
        }
    );
    if (!response.ok) {
      throw new Error('Failed to update bookmark');
    }
    const updated = await response.json();
    const idx = checkedOuts.value.findIndex((c) => c.id === updated.id);
    if (idx !== -1) {
      checkedOuts.value[idx].bookmark_page = updated.bookmark_page;
    }
    bookmarkDialog.value = false;
  } catch (err) {
    error.value = 'Something went wrong';
  }
}

</script>

<template>
  <h1 class="bg-grey-darken-4 text-h2 text-center pa-3  mb-5">Library</h1>
  <v-alert
      v-if="error"
      type="error"
      variant="tonal"
      class="mb-4"
  >
    {{ error }}
  </v-alert>
  <div>

    <p v-if="checkedOuts.length === 0" class="mx-5">You haven't checked out anything yet.</p>

    <v-container v-else class="">
      <v-card
          v-for="item in checkedOuts"
          :key="item.id"
          width="100%"
      >
        <v-card-title>{{ item.short_title }}</v-card-title>
        <v-card-subtitle>{{ item.author_name }}</v-card-subtitle>
        <v-card-text>
          <div>Page: {{ item.bookmark_page }}</div>
          <div>Last opened: {{ new Date(item.last_opened).toLocaleString() }}</div>
        </v-card-text>
        <v-card-actions>
          <v-container class="pa-0 ma-1">
            <v-row no-gutters>
              <v-col class="px-1">
                <v-hover v-slot="{isHovering, props}">
                  <v-btn block
                         icon="mdi-close"
                         rounded="0"
                         color="red-darken-4"
                         :variant="isHovering? 'elevated' : 'outlined'"
                         :class="{'on-hover': isHovering}"
                         v-bind="props"
                         @click="removeCheckout(item, $event)"
                  />
                </v-hover>
                <v-tooltip activator="parent" location="top">Remove from your Library</v-tooltip>
              </v-col>
              <v-col class="px-1">
                <v-hover v-slot="{isHovering, props}">
                  <v-btn block
                         icon="mdi-pencil-outline"
                         rounded="0"
                         color="blue-darken-4"
                         :variant="isHovering? 'elevated' : 'outlined'"
                         :class="{'on-hover': isHovering}"
                         v-bind="props"
                         @click="openBookmarkDialog(item, $event)"
                  />
                </v-hover>
                <v-tooltip activator="parent" location="top">Edit your Bookmark</v-tooltip>
              </v-col>
              <v-col class="px-1">
                <v-hover v-slot="{isHovering, props}">
                  <v-btn block
                         icon="mdi-arrow-top-right"
                         rounded="0"
                         color="green-darken-4"
                         :variant="isHovering? 'elevated' : 'outlined'"
                         :class="{'on-hover': isHovering}"
                         v-bind="props"
                         @click="openDocument(item)"
                  />
                </v-hover>
                <v-tooltip activator="parent" location="top">Go to Document</v-tooltip>
              </v-col>
            </v-row>
          </v-container>
        </v-card-actions>
      </v-card>
    </v-container>

    <v-dialog v-model="bookmarkDialog" max-width="400">
      <v-card>
        <v-card-title>Set bookmark page</v-card-title>
        <v-card-text>
          <v-text-field v-model.number="bookmarkInput" type="number" label="Page" />
        </v-card-text>
        <v-card-actions>
          <v-btn color="red-darken-4" variant="outlined" @click="bookmarkDialog = false">Cancel</v-btn>
          <v-btn color="green-darken-3" variant="elevated" @click="saveBookmark">Save</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>

  </div>
</template>