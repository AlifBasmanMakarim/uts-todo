<template>
  <div class="app">
    <h1 class="title">Kegabutan</h1>
    <div class="input-group">
      <input v-model="newTask" placeholder="Tambahkan kegiatan baru..." />
      <button @click="addTask">Tambah</button>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const newTask = ref('')

function addTask() {
  console.log('Tambah task:', newTask.value)
}
</script>

<style scoped>
/* style dari tahap sebelumnya tetap */

.input-group {
  display: flex;
  gap: 0.5rem;
}

.input-group input {
  flex: 1;
  padding: 0.5rem;
  border-radius: 8px;
  border: 1px solid #06a960;
  font-size: 1rem;
}

.input-group button {
  padding: 0.5rem 1rem;
  border: none;
  background-color: #3498db;
  color: white;
  border-radius: 8px;
  cursor: pointer;
  font-size: 1rem;
  transition: background-color 0.3s ease;
}

.input-group button:hover {
  background-color: #2980b9;
}
</style>