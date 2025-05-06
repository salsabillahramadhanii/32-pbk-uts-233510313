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