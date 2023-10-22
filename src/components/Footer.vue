<script setup lang="ts">
import { ref } from 'vue'

const history = ref([
  'KE1 <--------> EMPLOYEE1 at 20/10/2023 22:21:00',
  'KE2 <--------> EMPLOYEE2 at 20/10/2023 22:21:00'
])
</script>

<template>
  <footer>
    <ul v-if="history.length">
      <li v-for="item of history">{{ item }}</li>
    </ul>
  </footer>
</template>

<style scoped>
footer {
  padding: 2rem;
}

li {
  margin-bottom: 0.1rem;
  padding-left: 2rem;
  padding-top: 0.5rem;
  padding-bottom: 0.5rem;
  border: 1px solid black;
}
</style>
