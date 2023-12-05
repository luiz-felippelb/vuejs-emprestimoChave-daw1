<script setup lang="ts">
import { ref } from 'vue';
import axios from 'axios';

const props = defineProps({
  show: Boolean
})

const nomeChave = ref('');
const Message = ref('')

const cadastrarChave = async () => {
  if (nomeChave.value.trim() !== '') {
    try {
      Message.value = ''
      const response = await axios.post('http://localhost:3000/chave', { nome: nomeChave.value });

      // Lide com a resposta da API, por exemplo, exibindo uma mensagem de sucesso
      console.log('Chave cadastrada com sucesso:', response.data);

      // Limpar o campo de nome da chave após o cadastro
      nomeChave.value = '';

      Message.value = 'Chave cadastrada com sucesso'
    } catch (error) {
      Message.value = 'Chave já cadastrada'
      console.error('Erro ao cadastrar a chave:', error);
    }
  }
};

</script>

<template>
  <link rel="stylesheet" href="src/assets/modal.css">
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
            <button type="submit">Cadastrar</button>

            <p :class="{'visible': Message !== ''}" >{{ Message }}!</p>
          </form>
        </div>

        <button class="modal-default-button" @click="$emit('close')">X</button>
      </div>
    </div>
  </Transition>
</template>

<style scoped>
</style>