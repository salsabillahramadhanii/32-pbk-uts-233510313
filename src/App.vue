<template>
  <div>
    <h1>Catatan Aktivitas Harian</h1>
    <div class="input-group">
      <input v-model="newTodo" placeholder="Tambahkan kegiatan..." />
      <button @click="addTodo">Tambah</button>
    </div>

    <div class="filter-group">
      <label>
        <input type="checkbox" v-model="showOnlyUnfinished" />
        Tampilkan hanya yang belum selesai
      </label>
    </div>

    <ul>
      <li v-for="(task, index) in filteredTodos" :key="index">
        <input type="checkbox" v-model="task.completed" />
        <span :style="{ textDecoration: task.completed ? 'line-through' : 'none' }">
        {{ task.name }}
      </span>
        <button @click="removeTodo(index)">Batal</button>

      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

const tasks = ref([
  { name: 'Memasak', completed: false },
  { name: 'Belajar', completed: false }
])
const newTodo = ref('')
const showOnlyUnfinished = ref(false)

const addTodo = () => {
  if (newTodo.value.trim() !== '') {
    tasks.value.push({ name: newTodo.value, completed: false })
    newTodo.value = ''
  }
}
const removeTodo = (index) => {
  tasks.value.splice(index, 1)
}
const filteredTodos = computed(() => {
  if (showOnlyUnfinished.value) {
    return tasks.value.filter(task => !task.completed)
  }
  return tasks.value
})

</script>

<style>
body {
  font-family: 'Poppins', sans-serif;
  background-color: #2f4e39;
  margin: 0;
  padding: 20px 0;
  display: flex;
  justify-content: center;
  align-items: flex-start;
  min-height: 100vh;
}

div {
  background-color: #fffef9;
  border: 2px solid #ccc6b0;
  border-radius: 6px;
  padding: 20px;
  width: 90%;
  max-width: 450px;
  box-shadow: 0 0 8px rgba(0, 0, 0, 0.1);
  transition: box-shadow 0.3s ease;
}
div:hover {
  box-shadow: 0 0 12px rgba(0, 0, 0, 0.2);
}

h1 {
  text-align: center;
  font-size: 1.8rem;
  font-weight: 700;
  color: #3c2f2f;
  margin-bottom: 20px;
  line-height: 1.3;
}

.input-group {
  display: flex;
  margin-bottom: 15px;
  border: 4px solid #2f4e39;
  border-radius: 25px;
  overflow: hidden;
}
.input-group:focus-within {
  border-color: #1e3524;
}
.input-group input {
  flex: 1;
  padding: 8px 12px;
  font-size: 0.9rem;
  border: none;
  background-color: #c7c5b0;
  color: #3c2f2f;
  outline: none;
}
.input-group input:focus {
  background-color: #dcdac3;
}
.input-group button {
  background-color: #2f4e39;
  color: #fffef9;
  font-weight: bold;
  border: none;
  padding: 0 16px;
  font-size: 0.9rem;
  cursor: pointer;
  transition: background-color 0.3s ease, transform 0.2s;
}
.input-group button:hover {
  background-color: #24402f;
  transform: scale(1.05);
}

.filter-group {
  margin-bottom: 15px;
}
.filter-group label {
  font-weight: 600;
  font-size: 1rem;
  color: #3c2f2f;
  cursor: pointer;
}
.filter-group input[type='checkbox'] {
  margin-right: 8px;
  accent-color: #2f4e39;
  cursor: pointer;
}

ul {
  list-style: none;
  padding: 0;
  margin: 0;
}
li {
  background-color: #4c3d36;
  color: #fffef9;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 10px 12px;
  margin-bottom: 10px;
  border-radius: 8px;
  transition: transform 0.2s ease, background-color 0.3s;
}
li:hover {
  transform: translateY(-2px);
  background-color: #5d4a43;
}
li input[type='checkbox'] {
  margin-right: 8px;
  accent-color: #2f4e39;
  cursor: pointer;
}
li span {
  flex: 1;
  font-size: 0.95rem;
}
li button {
  background-color: #c7c5b0;
  color: #2f4e39;
  border: none;
  padding: 4px 12px;
  border-radius: 999px;
  font-weight: bold;
  font-size: 0.85rem;
  cursor: pointer;
  transition: background-color 0.3s ease, transform 0.2s ease;
}
li button:hover {
  background-color: #b0ad93;
  transform: scale(1.05);
}

</style>