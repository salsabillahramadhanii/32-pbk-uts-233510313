<template>
  <div>
    <h1>Catatan Aktivitas Harian</h1>
    <div class="input-group">
      <input v-model="newTodo" placeholder="Tambahkan kegiatan..." />
      <button @click="addTodo">Tambah</button>
    </div>

    <ul>
      <li v-for="(task, index) in tasks" :key="index">
        {{ task.name }}
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const tasks = ref([
  { name: 'Memasak', completed: false },
  { name: 'Belajar', completed: false }
])
const newTodo = ref('')

const addTodo = () => {
  if (newTodo.value.trim() !== '') {
    tasks.value.push({ name: newTodo.value, completed: false })
    newTodo.value = ''
  }
}

</script>