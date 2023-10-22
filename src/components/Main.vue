<script setup lang="ts">
import IconKey from './icons/IconKey.vue'
import { ref } from 'vue'

const listKey = ref(['KEY1', 'KEY2', 'KEY3', 'KEY4', 'KEY5'])
const listEmployee = ref(['EMPLOYEE1', 'EMPLOYEE2', 'EMPLOYEE3', 'EMPLOYEE4', 'EMPLOYEE5'])

const key = ref('')
const employee = ref('')

const msgConfirmation = ref('Empréstimo efetuado com sucesso!')
const show = ref(false)

function showConfirmation() {
  if(key.value != '' && employee.value != '')
    show.value = !show.value
}
</script>

<template>
  <main>
    <select v-model="key" id="selectKey">
      <option value="" disabled selected hidden>Selecione uma chave</option>
      <option v-for="key of listKey" :value="key">{{ key }}</option>
    </select>

    <button @click="showConfirmation">
      <IconKey></IconKey>
    </button>

    <select v-model="employee" id="selectEmployee">
      <option selected value="" disabled hidden>Selecione um servidor</option>
      <option v-for="employee of listEmployee" :value="employee">{{ employee }}</option>
    </select>

    <Transition name="slide">
      <div v-if="show" class="view">{{ msgConfirmation }}</div>
    </Transition>
  </main>
</template>

<style scoped>
main {
  display: flex;
  padding: 4rem;
  align-items: center;
  justify-content: space-around;
  border-bottom: 1px solid black;
}

select {
  cursor: pointer;
  appearance: none;
  padding: 1rem 4rem;
  border-radius: 2rem;
  text-align: center;
  font-size: 18px;
}

button {
  padding: 1rem;
  border-radius: 50%;
}

.view {
  border-radius: 2rem 0 0 2rem;
  position: fixed;
  top: 100px;
  right: 0;
  background-color: #4ddb6c;
  padding: 1.5rem 5rem 1.5rem 3rem;
  transition: left 0.5s;
}

.slide-enter-active {
  transition: all 0.5s ease-in-out;
}

.slide-leave-active {
  transition: all 0.5s ease-in-out;
}

.slide-enter-from, .slide-leave-to {
  transform: translateX(100px);
  opacity: 0;
}
</style>
