<script setup lang="ts">
import AddKey from './modals/AddKey.vue'
import { ref } from 'vue'

const title = ref('Where\'s the key?')

const showModal = ref(false)

</script>

<template>
  <header>
    <img class="logo" src="../assets/logo.png" alt="Key logo" width="150" height="150" />

    <div class="title">
      <h1>{{ title }}</h1>
    </div>

    <nav>
      <button @click="showModal = true"><img src="../assets/add-key.png" alt="Add key icon" width="60" height="60"></button>
      <button><img src="../assets/add-employee.png" alt="Add employee.png" width="60" height="60"></button>
    </nav>
  </header>

  <Teleport to="body">
    <AddKey :show="showModal" @close="showModal = false"></AddKey>
  </Teleport>
</template>

<style scoped>
header {
  display: flex;
  padding: 0.5rem 3rem 0.5rem 3em;
  align-items: center;
  background-color: #50BF84;
}

.title {
  font-size: 1.5rem;
  width: 80%;
}

h1 {
  padding-top: 1em;
}

nav {
  display: flex;
  padding-top: 3.5em;
  padding-right: 1rem;
}

button {
  margin-right: 1rem;
  cursor: pointer;
  background-color: transparent;
}

</style>
