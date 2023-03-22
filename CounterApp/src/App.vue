<script setup>
import {ref} from 'vue';

const count = ref(0);
const addToCounter = () => {
  count.value = count.value + 1
}
const subtractFromCounter = () => {
  count.value = count.value - 1
}
</script>

<template>
  <main class="main_content">
    <div class="content">
      <h1>The current count is: </h1>
      <h2> {{ count }}</h2>
      <!-- ddd --> 
      <button @click="subtractFromCounter">-</button>
      <button @click="addToCounter">+</button>
    </div>
  </main>
</template>

<style scoped>
  .main_content {
  /* No final de cada conjunto chave-valor é necessário adicionar o ponto e vírgula. */
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: rgb(24, 141, 106);
  } /* Não precisa colocar vírgula entre os seletores diferentes, basta por um abaixo do outro. */
  .content {
    text-align: center;
  }
</style>