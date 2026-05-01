<script setup>
import {onMounted, ref} from 'vue';
import DocumentCard from './documentCard.vue';
const loading = ref(true)   ;
const error = ref('')  ;
const itemsperpage = ref(10);
const documents = ref([])
const selectedDocument = ref(null);
const headers = [
  { title: 'Title', key: 'short_title', sortable: true },
  { title: 'Author', key: 'author_name', sortable: true },
];



async function loadDocuments() {
  loading.value = true;
  error.value = "";

  try {
    const response = await fetch("/api/documents")
    if(!response.ok) {
      throw new Error('failed to load documents')
    }

    const data = await response.json();
    documents.value = data.map((doc) =>({
      id: doc.id,
      title: doc.title,
      short_title: doc.short_title,
      year_published: doc.year_published,
      language: doc.language,
      author_id: doc.author_id,
      author_name: doc.author_name,
      link: doc.link,
    }))
  }
  catch(err) {
    error.value = "Something went wrong";
  }
  finally {
    loading.value = false;
  }
}

onMounted(() => {loadDocuments()})

function handleRowClick(_event, { item }) {
  selectedDocument.value = item;
}

</script>

<template>
  <h1 class="bg-grey-darken-4 text-h2 text-center pa-3  mb-5">Documents</h1>
  <v-alert
      v-if="error"
      type="error"
      variant="tonal"
      class="mb-4"
  >
    {{ error }}
  </v-alert>

  <v-row class="mx-5">
    <v-col cols="12" md="8">
      <v-data-table
          v-model:items-per-page="itemsperpage"
          :headers="headers"
          :items="documents"
          :loading="loading"
          item-value="id"
          hover
          @click:row="handleRowClick"
      />
    </v-col>

    <v-col cols="12" md="4">
      <DocumentCard
          v-if="selectedDocument"
          :id="selectedDocument.id"
          :title="selectedDocument.title"
          :short_title="selectedDocument.short_title"
          :year_published="selectedDocument.year_published"
          :language="selectedDocument.language"
          :author_id="selectedDocument.author_id"
          :author_name="selectedDocument.author_name"
          :link="selectedDocument.link"
      />
      <v-card v-else variant="tonal" class="text-center pa-6">
        <v-card-text class="text-medium-emphasis">
          Select a document to see details
        </v-card-text>
      </v-card>
    </v-col>
  </v-row>

</template>