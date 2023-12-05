<script setup lang="ts">
import { ref, getCurrentInstance } from 'vue';
import axios from 'axios';

const props = defineProps({
    show: Boolean
})

const nomeChave = ref('')
const Message = ref('')

const buscarChave = async () => {
    if (nomeChave.value.trim() !== '') {
        try {
            Message.value = ''
            const response = await axios.get(`http://localhost:3000/chave/${nomeChave.value}`);
            console.log('Chave: ', response.data);
            // Emitir evento para o componente pai com o valor da chave
            const instance = getCurrentInstance();
            if (instance) {
                instance.emit('chave-encontrada', response.data);
            }
            Message.value = 'Chave selecionada'
        } catch (error) {
            Message.value = 'Chave não encontrada'
            console.error('Erro ao buscar a chave no banco', error);
        }
    }
}
</script>  

<template>
    <link rel="stylesheet" href="src/assets/modal.css">
    <Transition name="modal">
        <div v-if="show" class="modal-mask">
            <div class="modal-container">

                <div class="modal-header">
                    <h3>Buscar chave</h3>
                </div>

                <div class="modal-body">
                    <form @submit.prevent="buscarChave">
                        <label for="nomeChave">Nome da Chave:</label>
                        <input type="text" id="nomeChave" v-model="nomeChave" required>
                        <button type="submit">Buscar</button>
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