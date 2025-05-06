<template>
  <div>
    <h1>Catatan Aktivitas Harian</h1>
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
</script>