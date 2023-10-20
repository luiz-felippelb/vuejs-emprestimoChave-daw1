<script setup lang="ts">
import IconKey from './icons/IconKey.vue';
import { ref } from 'vue';

const listKey = ref(['KEY1', 'KEY2', 'KEY3', 'KEY4', 'KEY5'])
const listEmployee = ref(['EMPLOYEE1', 'EMPLOYEE2', 'EMPLOYEE3', 'EMPLOYEE4', 'EMPLOYEE5'])

const key = ref('')
const employee = ref('')

</script>

<template>
    <main>
        <select v-model="key" id="selectKey">
            <option value="" disabled selected hidden>Selecione uma chave</option>
            <option v-for="key of listKey" :value="key">{{ key }}</option>
        </select>

        <button @click="">
            <IconKey></IconKey>
        </button>

        <select v-model="employee" id="selectEmployee">
            <option selected value="" disabled hidden>Selecione um servidor</option>
            <option v-for="employee of listEmployee" :value="employee">{{ employee }}</option>
        </select>
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

</style>