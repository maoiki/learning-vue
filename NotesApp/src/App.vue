<script setup>
import {ref} from 'vue';

const showModal = ref(false);
const newNote = ref("");
const notes = ref([]);
const errorMessage = ref("");

const randomBackgroundColor = () => {
  return "hsl(" + (Math.random() * 360) + ", 75%, 75%"
}

const resetModal = () => {
  showModal.value = false;
  newNote.value = "";
  errorMessage.value = "";
}

const addNote = () => {
  if(!newNote.value.length){
    errorMessage.value = "Field cannot be empty."
    return
  }
  else{
    notes.value.push({

      id: Date.now(),
      text: newNote.value,
      date: new Date(),
      bgColor: randomBackgroundColor()
    });

    resetModal()
  }
}
const removeNote = (index) => {
  console.log(index)
  notes.value.splice(index, 1)
};
</script>

<template>
<main>
  <div v-if="showModal" class="overlay">
    <div class="modal">
      <h2>Write your note here: </h2>
      <textarea v-model.trim="newNote" name="note" id="note" cols="20" rows="10"></textarea>
      <p class="invalid" v-if="errorMessage"> {{ errorMessage }}</p>
      <div class="buttons-container">
        <button class="button-add" @click="addNote"> Add note </button>
        <button class="button-cancel" @click="resetModal"> Cancel </button>
      </div>
    </div>
  </div>

  <div class="container">
    <header>
      <h1>Notes </h1>
      <button class="header-button" @click="showModal = true">+</button>
    </header>
    <div class="cards-container">
      <div
        v-if="notes.length > 0" 
        v-for="note, index in notes" 
        class="card" 
        :style="{backgroundColor: note.bgColor}"
        :key="note.id"
        >
        <p class="main-text"> {{note.text}} </p>
        <div class="card-bottom">
          <p class="date"> {{note.date.toLocaleDateString('pt-br')}} </p>
          <span class="delete" @click="removeNote(index)">🗑️</span>
        </div>
      </div>
      <div v-else class="card">
        <p class="main-text"> Hi, this is a default note! Write your own by clicking on the + button to your right :)</p>
      </div>
    </div>
  </div>
</main>
<footer><a class="link_externo" href="https://github.com/maoiki" target="_blank">Made with ♥ by Julio Duarte</a> </footer>
</template>

<style scoped>

  main{
    width: 100vw;
    height: 100vh;
  }

  footer{
    position:fixed;
    left: 0;
    bottom: 0;
    width: 100%;
    text-align: center;
    padding:10px;
    background-color: #41b883;
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
  a {
    text-decoration: none;
    color: var(--color-text);
  }
  .header-button {
    border: none;
    padding: 10px;
    width: 50px;
    height: 50px;
    cursor: pointer;
    background-color: #41b883;
    border-radius: 1000px;
    color: white;
    font-size: 20px;
  }

  .card {
    width: 225px;
    height: 225px;
    padding: 10px;
    border-radius: 15px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    margin-right: 20px;
    margin-bottom: 20px;
    background-color: #41b883;
  }
  .card-bottom{
    display: flex;
    flex-direction: row;
    justify-content: space-between;
  }
  .main-text {
    line-height: 1.25;
    font-size: 17.5px;
    font-weight: bold;
  }
  .date {
    font-size: 15px;
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
  .buttons-container{
    display: flex;
    gap: 20px;
    justify-content: center;
  }
  .button-add {
    padding: 10px 20px;
    font-size: 20px;
    width: fit-content;
    background-color: #41b883;
    border: none;
    color: white;
    cursor: pointer;
    margin-top: 15px;
    border-radius: 15px;
  }
  .button-cancel {
    padding: 10px 20px;
    font-size: 20px;
    width: fit-content;
    border:none;
    color: rgb(255, 255, 255);
    cursor: pointer;
    margin-top: 15px;
    border-radius: 15px;
    background-color: rgb(182, 190, 188);
  }

  .delete{
    display: flex;
    font-size: 15px;
    cursor: pointer;
    background-color: rgba(255, 255, 255, 0.753);
    border-radius: 50px;
    height: 30px;
    width: 30px;
    justify-content: center;
    align-items: center;
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
    
    resize: none
  }

  textarea:focus{
    outline: none;
    border-color:#41b883;
  }

  .cards-container {
    display: flex;
    flex-wrap: wrap;
  }

</style>