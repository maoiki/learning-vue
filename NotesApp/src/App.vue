<script setup>
import {ref} from 'vue';

const showModal = ref(false);
const newNote = ref("");
const notes = ref([]);
const errorMessage = ref("");

const randomBackgroundColor = () => {
  return "hsl(" + (Math.random() * 360) + ", 75%, 75%"
}

const addNote = () => {
  // validação básica para que não seja criada uma nota vazia
  if(!newNote.value.length){
    errorMessage.value = "Campo não pode estar vazio."
    return
  }
    notes.value.push({
      // para gerar um id único usarei Date.now() por servir para o caso, mas provavelmente um UUID se sairia melhor em algumas situações
      id: Date.now(),
      text: newNote.value,
      date: new Date(),
      bgColor: randomBackgroundColor()
    });
    // esse pedaço em essência só sai "resetando" tudo, certamente existe alguma forma mais elegante de implementar isso
    showModal.value = false;
    newNote.value = "";
    errorMessage.value = "";
  
}
</script>

<template>
<main>
  {{ notes }}
  <div v-if="showModal" class="overlay">
    <div class="modal">
      <button class="close" @click="showModal = false"> X </button>
      <textarea v-model.trim="newNote" name="note" id="note" cols="20" rows="10"></textarea>
      <p class="invalid" v-if="errorMessage"> {{ errorMessage }}</p>
      <button class="add_note" @click="addNote"> Add note </button>
    </div>
  </div>

  <div class="container">
    <header>
      <h1>Notes </h1>
      <button class="header_button" @click="showModal = true">+</button>
    </header>
    <div class="cards-container">
      <div 
        v-for="note in notes" 
        class="card" 
        :style="{backgroundColor: note.bgColor}"
        :key="note.id"
        >
        <p class="main-text"> {{note.text}} </p>
        <p class="date"> {{note.date.toLocaleDateString('pt-br')}} </p>
      </div>
    </div>
  </div>
</main>
</template>

<style scoped>
  main {
    height: 100vh;
    width: 100vw;
  }
  .container {
    max-width: 1000px;
    padding: 10px;
    margin: 0 auto
  }
  header {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  h1 {
    font-weight: bold;
    margin-bottom: 25px;
    font-size: 75px;
  }
  .header_button {
    border: none;
    padding: 10px;
    width: 50px;
    height: 50px;
    cursor: pointer;
    background-color: hsla(160, 100%, 37%, 1);
    border-radius: 1000px;
    color: white;
    font-size: 20px;
  }

  .card {
    width: 225px;
    height: 225px;
    background-color: rgb(237, 182, 44);
    padding: 10px;
    border-radius: 15px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    margin-right: 20px;
    margin-bottom: 20px;
  }
  .main-text {
    line-height: 1.25;
    font-size: 17.5px;
    font-weight: bold;
  }
  .date {
    font-size: 12.5px;
    margin-top: auto;
  }
  .overlay {
    position: absolute;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.77);
    transform: translate(-50%, -50%);
    top: 50%;
    left: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    z-index: 10;
  }
  .modal {
    width: 750px;
    background-color: white;
    border-radius: 10px;
    padding: 30px;
    position: relative;
    display: flex;
    flex-direction: column;
  }
  .add_note {
    padding: 10px 20px;
    font-size: 20px;
    width: 100%;
    background-color: hsla(160, 100%, 37%, 1);
    border: none;
    color: white;
    cursor: pointer;
    margin-top: 15px;
    border-radius: 15px;
  }
  .invalid {
    margin-left: auto;
    font-size: 14px;
    font-weight: bold;
    color:#dc3545;
  }

  textarea {
    width: 100%;
    height: 200px;
    padding: 5px;
    font-size: 20px;
    border-radius: 2px;
    resize: none
  }

  .cards-container {
    display: flex;
    flex-wrap: wrap;
  }

</style>