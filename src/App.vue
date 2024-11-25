<template>
  <div class="container">
    <h1>Выбор папки</h1>
    <span v-if="selectedId !== null">Выбрана папка с id: {{ selectedId }}</span><br />
    <button @click="showModal = true">Открыть</button>
    <Modal :isVisible="showModal" title="Выберите папку" :folders="mockFolders" @close="showModal = false"
      @select="handleSelect" />
  </div>
</template>


<script setup lang="ts">
import { ref } from 'vue';
import { Folder } from './types';
import Modal from '../src/components/Modal.vue';

const mockFolders: Folder[] = [
  {
    id: 1, name: 'Папка 1', children: [
      { id: 2, name: 'Папка 1.1', children: [] },
      {
        id: 3, name: 'Папка 1.2', children: [
          { id: 4, name: 'Папка 1.2.1', children: [] }
        ]
      }
    ]
  },
  { id: 5, name: 'Папка 2', children: [] },
];

const showModal = ref(false);
const selectedId = ref<number | null>(null);

const handleSelect = (id: number) => {
  console.log('Выбрана папка с id:', id);
  selectedId.value = id;
  showModal.value = false;
};

</script>

<style>
body {
  font-family: 'Helvetica', sans-serif;
  background-color: #f9f9f9;
  margin: 0;
  padding: 0;
}

.container {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
  box-shadow: 0 2px 15px rgba(0, 0, 0, 0.1);
  border-radius: 10px;
  background-color: #ffffff;
}
</style>