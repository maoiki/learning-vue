<script setup>
import {ref} from 'vue'

const count = ref(0)
const addToCounter = () => {
  count.value += 1
}
const subtractFromCounter = () => {
  count.value -= 1
}
;
</script>

<template>
  <main class="main_content">
    <div class="content">
      <h1>The current count is: </h1>
      <p> {{ count }}</p>
      <button @click="subtractFromCounter">-</button>
      <button @click="addToCounter">+</button>
      <footer><a class="link_externo" href="https://github.com/maoiki" target="_blank">Made with ♥ by Julio Duarte</a></footer>
    </div>
  </main>
</template>

<style scoped>

  .main_content {
    height: 100vh;
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
  } 
  .content {
    text-align: center;
    width:fit-content;
    padding: 40px;
    border-radius: 50px;
    background-color: #41b883;
  }
  
  button {
    font-size: 20px;
    height: 35px;
    width: 35px;
    margin: 5px 5px 35px 10px;
  }

  p{
    font-size:40px;
  }
  a {
    align-self: end;
    text-decoration: none;
    color: var(--color-text);
  }
</style>