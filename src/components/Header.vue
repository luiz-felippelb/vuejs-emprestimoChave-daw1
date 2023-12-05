<script setup lang="ts">
import BuscarChave from './modals/BuscarChave.vue';
import AddKey from './modals/AddKey.vue'
import AlterarChave from './modals/AlterarChave.vue';
import RemoverChave from './modals/RemoverChave.vue';
import { ref } from 'vue'

const title = ref('Where\'s the key?')

const showModalAdd = ref(false)
const showModalFind = ref(false)
const showModalEdit = ref(false)
const showModalDelete = ref(false)

</script>

<template>
  <header>
    <img class="logo" src="../assets/logo.png" alt="Key logo" width="150" height="150" />

    <div class="title">
      <h1>{{ title }}</h1>
    </div>

    <nav>
      <div class="dropdown">
        <button class="dropbtn"><img src="../assets/key.png" alt="Key icon" width="50"
            height="50"><span>Chaves</span></button>
        <div class="dropdown-content">
          <a @click="showModalAdd = true" title="Inserir"><span>Inserir</span><img src="../assets/add.png"
              alt="Add key icon"></a>
          <a @click="showModalFind = true" title="Buscar"><span>Buscar</span><img src="../assets/find.png"
              alt="Add key icon"></a>
          <a @click="showModalEdit = true" title="Alterar"><span>Alterar</span><img src="../assets/edit.png"
              alt="Add key icon"></a>
          <a @click="showModalDelete = true" title="Remover"><span>Remover</span><img src="../assets/remove.png"
              alt="Add key icon"></a>
        </div>
      </div>
    </nav>
  </header>

  <Teleport to="body">
    <AddKey :show="showModalAdd" @close="showModalAdd = false"></AddKey>
    <BuscarChave :show="showModalFind" @close="showModalFind = false"></BuscarChave>
    <AlterarChave :show="showModalEdit" @close="showModalEdit = false"></AlterarChave>
    <RemoverChave :show="showModalDelete" @close="showModalDelete = false"></RemoverChave>
  </Teleport>
</template>


<style scoped>
header {
  display: flex;
  padding: 0.5rem 3rem 0.5rem 3rem;
  align-items: center;
  background-color: #50BF84;
}

.title {
  font-size: 2rem;
  width: 80%;
}

h1 {
  margin-top: auto;
  margin-left: 1rem;
}

/* Style The Dropdown Button */
.dropbtn {
  padding: 5px;
  margin-top: auto;
  background-color: transparent;
  display: flex;
  align-items: center;
  width: 9rem;
}

.dropbtn span {
  margin-left: 0.5rem;
  font-size: 1rem;
}

/* The container <div> - needed to position the dropdown content */
.dropdown {
  position: relative;
  display: inline-block;
}

/* Dropdown Content (Hidden by Default) */
.dropdown-content {
  display: none;
  position: absolute;
  background-color: white;
  box-shadow: 0px 8px 16px 0px rgba(0, 0, 0, 0.2);
  z-index: 1;
}

/* Links inside the dropdown */
.dropdown-content a {
  position: relative;
  color: black;
  padding: 10px;
  text-decoration: none;
  display: block;
  width: 9rem;
}

.dropdown-content a img {
  width: 40px;
  height: 40px;
}

.dropdown-content a span {
  position: absolute;
  top: 1.3rem;
  left: 4rem;
  font-size: 1rem;
}

/* Change color of dropdown links on hover */
.dropdown-content a:hover {
  background-color: #B3DE5D;
  cursor: pointer;
}

/* Show the dropdown menu on hover */
.dropdown:hover .dropdown-content {
  display: block;
}

/* Change the background color of the dropdown button when the dropdown content is shown */
.dropdown:hover .dropbtn {
  background-color: #B3DE5D;
}</style>