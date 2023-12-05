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

const removerChave = async () => {
    if (key.value.trim() !== '') {
        try {
            Message.value = '';
            const chaveSelecionada = listKey.value.find((chave) => chave.nome === key.value);

            if (chaveSelecionada) {
                const response = await axios.patch(`http://localhost:3000/chave/desativar/${chaveSelecionada.nome}`);

                // Lide com a resposta da API, por exemplo, exibindo uma mensagem de sucesso
                console.log('Chave removida com sucesso:', response.data);

                // Atualizar a lista de chaves após a remoção
                fetchData();

                // Limpar os campos após a remoção
                key.value = '';
                Message.value = 'Chave removida';
            } else {
                Message.value = 'Chave não encontrada';
            }
        } catch (error) {
            Message.value = 'Erro ao remover a chave';
            console.error('Erro ao remover a chave no banco', error);
        }
    } else {
        Message.value = 'Selecione uma chave para remover';
    }
};
</script>

<template>
    <link rel="stylesheet" href="src/assets/modal.css">
    <Transition name="modal">
        <div v-if="show" class="modal-mask">
            <div class="modal-container">

                <div class="modal-header">
                    <h3>Remover Chave</h3>
                </div>

                <div class="modal-body">
                    <form @submit.prevent="removerChave">
                        <select v-model="key" id="selectKey">
                            <option value="" disabled selected hidden>Selecione uma chave</option>
                            <option v-for="chave in listKey" :value="chave.nome">{{ chave.nome }}</option>
                        </select>

                        <button type="submit">Remover</button>

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
