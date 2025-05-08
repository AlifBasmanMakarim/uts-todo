<template>
  <div class="app">
    <h1 class="title">Kegabutan</h1>
    <div class="input-group">
      <input v-model="newTask" @keyup.enter="addTask" placeholder="Tambahkan kegiatan baru..." />
      <button @click="addTask">Tambah</button>
    </div>

    <div class="filter">
      <label>
        <input type="checkbox" v-model="showOnlyIncomplete" />
        Tampilkan hanya yang belum selesai
      </label>
    </div>

    <ul class="task-list">
      <li v-for="(task, index) in filteredTasks" :key="index" class="task-item">
        <input type="checkbox" v-model="task.completed" class="checkbox" />
        <span :class="{ completed: task.completed }">{{ task.text }}</span>
        <button class="delete" @click="removeTask(index)">Batal</button>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

const newTask = ref('')
const tasks = ref([])
const showOnlyIncomplete = ref(false)

function addTask() {
  if (newTask.value.trim()) {
    tasks.value.push({ text: newTask.value, completed: false })
    newTask.value = ''
  }
}

function removeTask(index) {
  tasks.value.splice(index, 1)
}

const filteredTasks = computed(() => {
  return showOnlyIncomplete.value
    ? tasks.value.filter(task => !task.completed)
    : tasks.value
})
</script>

<style scoped>
.app {
  max-width: 500px;
  margin: 2rem auto;
  padding: 1.5rem;
  border-radius: 12px;
  background: rgb(0, 21, 5);
  box-shadow: 0 4px 10px rgba(2, 166, 172, 0.904);
  font-family: 'Segoe UI', sans-serif;
}

.title {
  text-align: center;
  color: #d4df07;
  margin-bottom: 1rem;
}

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

.filter {
  margin: 1rem 0;
  text-align: center;
  color: white;
}

.task-list {
  list-style: none;
  padding: 0;
}

.task-item {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.5rem 0;
  border-bottom: 1px solid #3607e1;
  color: white;
}

.task-item span {
  flex: 1;
  font-size: 1rem;
}

.task-item span.completed {
  text-decoration: line-through;
  color: #ff0000;
}

.task-item .checkbox {
  accent-color: #27ae60;
  width: 1rem;
  height: 1rem;
}

.task-item .delete {
  background-color: #e74c3c;
  color: white;
  border: none;
  padding: 0.3rem 0.7rem;
  border-radius: 6px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.task-item .delete:hover {
  background-color: #c0392b;
}
</style>