<script setup lang="ts">
import BuscarChave from './modals/BuscarChave.vue';
import { ref, onMounted, onUpdated } from 'vue'
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

// const fetchDataServidor = async () => {
//   try {
//     const response = await axios.get('http://localhost:3000/servidor')
//     listEmployee.value = response.data as Servidor[]
//   } catch(error) {
//     console.error("Erro na requisição à API: ", error)
//   }
// }

const msgConfirmation = ref('Empréstimo efetuado com sucesso!')
const show = ref(false)

function showConfirmation() {
  if(key.value != '' && employee.value != '')
    show.value = !show.value
}

onMounted(() => {
  fetchDataChave()
  //fetchDataServidor()
})

onUpdated(() => {
  fetchDataChave()
  //fetchDataServidor()
})

const chaveRetornada = (chave: Chave) => {
  key.value = chave.nome;
};

</script>

<template>
  <main>
    <BuscarChave @chave-encontrada="chaveRetornada"></BuscarChave>

    <select v-model="key" id="selectKey">
      <option value="" disabled hidden>Selecione uma chave</option>
      <option v-for="chave in listKey" :value="chave.nome">
        {{ chave.nome }}
      </option>
    </select>

    <button @click="showConfirmation">
      <img src="../assets/hands.png" alt="logo hands with key" width="70" height="70">
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
}

select {
  cursor: pointer;
  appearance: none;
  padding: 1rem 4rem;
  border-radius: 2rem;
  text-align: center;
  font-size: 18px;
  background-color: #50BF84;
}

select:hover {
  background-color: #B3DE5D;
}

button {
  padding: 1rem;
  border-radius: 50%;
  background-color: #50BF84;
}

.view {
  border-radius: 2rem 0 0 2rem;
  position: fixed;
  top: 200;
  right: 0;
  background-color: #B3DE5D;
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
