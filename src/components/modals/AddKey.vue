<script setup lang="ts">
import { ref } from 'vue';
import axios from 'axios';

const props = defineProps({
  show: Boolean
})

const nomeChave = ref('');

const cadastrarChave = async () => {
  if (nomeChave.value.trim() !== '') {
    try {
      const response = await axios.post('http://localhost:3000/chave', { nome: nomeChave.value});

      // Lide com a resposta da API, por exemplo, exibindo uma mensagem de sucesso
      console.log('Chave cadastrada com sucesso:', response.data);

      // Limpar o campo de nome da chave após o cadastro
      nomeChave.value = '';
    } catch (error) {
      console.error('Erro ao cadastrar a chave:', error);
    }
  }
};

</script>

<template>
  <Transition name="modal">
    <div v-if="show" class="modal-mask">
      <div class="modal-container">

        <div class="modal-header">
          <h3>Cadastro de Chave</h3>
        </div>

        <div class="modal-body">
          <form @submit.prevent="cadastrarChave">
            <label for="nomeChave">Nome da Chave:</label>
            <input type="text" id="nomeChave" v-model="nomeChave" required>
            <button id="button-form" type="submit">Cadastrar</button>
          </form>
        </div>

        <div class="modal-footer">
          <button class="modal-default-button" @click="$emit('close')"> X </button>
        </div>

      </div>
    </div>
  </Transition>
</template>

<style scoped>

input {
  display: block;
  border: 1px solid black;
  margin-top: 0.3rem;
  padding: 0.5rem;
}

#button-form {
  margin: auto;
  margin-top: 2rem;
  background-color: #42b983;
  border-radius: 2rem;
  padding: 0.5rem 1.5rem;
  cursor: pointer;
}

.modal-mask {
  position: fixed;
  z-index: 9998;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  transition: opacity 0.3s ease;
}

.modal-container {
  width: 300px;
  margin: auto;
  padding: 20px 30px;
  background-color: #fff;
  border-radius: 5px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
  transition: all 0.3s ease;
}

.modal-header h3 {
  margin-top: 0;
  color: #45A452;
}

.modal-body {
  margin: 20px 0;
}

.modal-default-button {
  cursor: pointer;
  position: fixed;
  top: 20px;
  right: 20px;
  background-color: #B05E31;
  border-radius: 2rem;
  padding: 0.5rem 1.5rem;
}

.modal-enter-from {
  opacity: 0;
}

.modal-leave-to {
  opacity: 0;
}

.modal-enter-from .modal-container,
.modal-leave-to .modal-container {
  -webkit-transform: scale(1.1);
  transform: scale(1.1);
}
</style>