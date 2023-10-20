<script setup lang="ts">
import { ref, inject } from 'vue';

const title = ref('Where is the key?')
const msgConfirmation = ref('Empréstimo efetuado com sucesso!')
const isView = ref(true)

function showConfirmation() {
    isView.value = !isView.value
}
</script>

<template>
    <header>
        <img class="logo" src="../assets/logo.png" alt="Key logo" width="200" height="200" />

        <div class="title">
            <h1>{{ title }}</h1>
        </div>

        <Transition name="slide">
            <div class="view">{{ msgConfirmation }}</div>
        </Transition>
    </header>
</template>

<style scoped>

header {
    display: flex;
    padding: 2rem;
    align-items: center;
    background-color: #54F0E0;
    border-bottom: 1px solid black;
}

.title {
    font-size: 1.5rem;
    padding: 0 2rem;
}

.view {
    border-radius: 2rem 0 0 2rem;
    position: fixed;
    right: 0;
    background-color: #4DDB6C;
    padding: 1.5rem;
    transition: left 0.5s;
}

.slide-enter-active, .slide-leave-active {
    transition: opacity 0.5s ease-in;
}
.slide-enter-from, .slide-leave-to {
    opacity: 0;
}

</style>