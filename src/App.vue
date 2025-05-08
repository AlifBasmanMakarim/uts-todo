<template>
  <div class="app">
    <h1 class="title">Kegabutan</h1>
    <div class="input-group">
      <input v-model="newTask" @keyup.enter="addTask" placeholder="Tambahkan kegiatan baru..." />
      <button @click="addTask">Tambah</button>
    </div>

    <ul class="task-list">
      <li v-for="(task, index) in tasks" :key="index" class="task-item">
        {{ task.text }}
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const newTask = ref('')
const tasks = ref([])

function addTask() {
  if (newTask.value.trim()) {
    tasks.value.push({ text: newTask.value, completed: false })
    newTask.value = ''
  }
}
</script>

<style scoped>
/* Tambahkan */
.task-list {
  list-style: none;
  padding: 0;
}

.task-item {
  padding: 0.5rem 0;
  border-bottom: 1px solid #3607e1;
  color: white;
}
</style>