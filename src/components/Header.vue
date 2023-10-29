<script setup lang="ts">
import { ref } from 'vue'

const title = ref('Where is the key?')

const isView = ref(true)

</script>

<template>
  <header>
    <img class="logo" src="../assets/logo.png" alt="Key logo" width="200" height="200" />

    <div class="title">
      <h1>{{ title }}</h1>
    </div>

  </header>
</template>

<style scoped>
header {
  display: flex;
  padding: 0.5rem 4rem 0.5rem 4rem;
  align-items: center;
  background-color: #54f0e0;
  border-bottom: 1px solid black;
}

.title {
  font-size: 2rem;
  padding: 0 2rem;
}
</style>
