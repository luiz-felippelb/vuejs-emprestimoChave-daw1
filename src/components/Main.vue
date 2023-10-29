<script setup lang="ts">
import IconKey from './icons/IconKey.vue'
import { ref, onMounted } from 'vue'
import axios from 'axios';

interface Chave {
  nome: string;
  situacao: string;
  status: boolean
}

interface Servidor {
  nome: string;
  cpf: string;
  contato: string;
  nascimento: Date,
  status: boolean
}

const listKey = ref<Chave[]>([]) 
const listEmployee = ref<Servidor[]>([])

const key = ref('')
const employee = ref('')

const fetchDataChave = async () => {
  try {
    const response = await axios.get('http://localhost:3000/chave')
    listKey.value = response.data as Chave[]
  } catch(error) {
    console.error("Erro na requisição à API: ", error)
  }
}

const fetchDataServidor = async () => {
  try {
    const response = await axios.get('http://localhost:3000/servidor')
    listEmployee.value = response.data as Servidor[]
  } catch(error) {
    console.error("Erro na requisição à API: ", error)
  }
}

const msgConfirmation = ref('Empréstimo efetuado com sucesso!')
const show = ref(false)

function showConfirmation() {
  if(key.value != '' && employee.value != '')
    show.value = !show.value
}

onMounted(() => {
  fetchDataChave()
  fetchDataServidor()
})

</script>

<template>
  <main>
    <select v-model="key" id="selectKey">
      <option value="" disabled selected hidden>Selecione uma chave</option>
      <option v-for="chave in listKey" :value="chave">{{ chave.nome }}</option>
    </select>

    <button @click="showConfirmation">
      <IconKey></IconKey>
    </button>

    <select v-model="employee" id="selectEmployee">
      <option selected value="" disabled hidden>Selecione um servidor</option>
      <option v-for="employee in listEmployee" :value="employee">{{ employee.nome }}</option>
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
