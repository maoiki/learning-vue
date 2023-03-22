<script setup>
import {RouterLink} from "vue-router"
const { numberofCorrectAnswers, 
        quizQuestionLength 
        } = defineProps(['numberofCorrectAnswers','quizQuestionLength']);
</script>

<template>
  <div class="results">
    <p>Your results...</p>
    <h1>{{ numberofCorrectAnswers }} / {{ quizQuestionLength }}</h1>
    <RouterLink class="buttonGoBack" to="/">Go back</RouterLink>
  </div>
</template>

<style scoped>
  .results {
    text-align: center;
    margin-top: 100px;
  }
  .buttonGoBack {
    font-size: 25px;
    text-decoration: none;
    border-radius: 50px;
    border-width: 4px;
    color: var(--color-text);
    background-color: #41b883;
    padding: 10px 20px;
  }
  p {
    font-size: 25px;
  }
  h1 {
    font-size: 80px;
    margin-bottom: 20px;
  }
</style>