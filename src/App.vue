<template>
  <div>
    <h1>Daftar Kegiatan</h1>
    <ul>
      <li v-for="(task, index) in filteredTodos" :key="index">
        {{ task.name }}

      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

const tasks = ref([
  { name: 'makan', completed: false },
  { name: 'minum', completed: false }
])
</script>