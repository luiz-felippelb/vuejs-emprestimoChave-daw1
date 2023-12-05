<script setup lang="ts">
import { ref, onMounted, onUpdated, defineProps } from 'vue';
import axios from 'axios';

interface Chave {
    nome: string;
    situacao: string;
    status: boolean;
}

const props = defineProps({
    show: Boolean,
});

const key = ref('');
const listKey = ref<Chave[]>([]);

const fetchData = async () => {
    try {
        const response = await axios.get('http://localhost:3000/chave');
        listKey.value = response.data as Chave[];
    } catch (error) {
        console.error('Erro na requisição à API: ', error);
    }
};

onMounted(() => {
    fetchData();
});

onUpdated(() => {
    fetchData();
});

const nomeChave = ref('');
const Message = ref('');

const alterarNomeChave = async () => {
    if (key.value.trim() !== '' && nomeChave.value.trim() !== '') {
        try {
            Message.value = '';
            const chaveSelecionada = listKey.value.find((chave) => chave.nome === key.value);

            if (chaveSelecionada) {
                const response = await axios.put(`http://localhost:3000/chave/${chaveSelecionada.nome}`, {
                    nome: nomeChave.value,
                });

                // Lide com a resposta da API, por exemplo, exibindo uma mensagem de sucesso
                console.log('Nome da chave alterado com sucesso:', response.data);

                // Atualizar a lista de chaves após a alteração
                fetchData();

                // Limpar os campos após a alteração
                key.value = '';
                nomeChave.value = '';
                Message.value = 'Nome alterado com sucesso';
            } else {
                Message.value = 'Chave não encontrada';
            }
        } catch (error) {
            Message.value = 'Erro ao alterar o nome da chave';
            console.error('Erro ao alterar o nome da chave no banco', error);
        }
    } else {
        Message.value = 'Selecione uma chave e forneça um novo nome';
    }
};
</script>

<template>
    <link rel="stylesheet" href="src/assets/modal.css">
    <Transition name="modal">
        <div v-if="show" class="modal-mask">
            <div class="modal-container">

                <div class="modal-header">
                    <h3>Editar Chave</h3>
                </div>

                <div class="modal-body">
                    <form @submit.prevent="alterarNomeChave">
                        <select v-model="key" id="selectKey">
                            <option value="" disabled selected hidden>Selecione uma chave</option>
                            <option v-for="chave in listKey" :value="chave.nome">{{ chave.nome }}</option>
                        </select>

                        <label for="nomeChave">Novo Nome da Chave:</label>
                        <input type="text" id="nomeChave" v-model="nomeChave" required>
                        <button type="submit">Alterar</button>

                        <p :class="{'visible': Message !== ''}" >{{ Message }}.</p>
                    </form>
                </div>

                <button class="modal-default-button" @click="$emit('close')">X</button>
            </div>
        </div>
    </Transition>
</template>

<style scoped>
</style>
