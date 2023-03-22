<script setup>
import { useRoute } from "vue-router"
import { ref, computed } from "vue"

import quizes from "../data/quizes.json"
import Question from "../components/Question.vue"
import QuizHeader from "../components/QuizHeader.vue"
import Results from "../components/Results.vue"
import Footer from "../components/Footer.vue" 

const route = useRoute()
const quizId = parseInt(route.params.id)
const quiz = quizes.find(q => q.id === quizId)
const numberofCorrectAnswers = ref(0)
const currentQuestionIndex = ref(0)
const showResults = ref(false)

const questionStatus = computed( () => `${currentQuestionIndex.value}/${quiz.questions.length}`)
const barPercentage = computed( () => `${currentQuestionIndex.value/quiz.questions.length * 100}%`)



const onOptionSelected = (isCorrect) => {
  if(isCorrect){
    numberofCorrectAnswers.value++
  }
  if(quiz.questions.length - 1 === currentQuestionIndex.value){
    showResults.value = true
  }
  currentQuestionIndex.value++
}

;
</script>

<template>
  <div>
    <QuizHeader 
      :questionStatus="questionStatus"
      :barPercentage="barPercentage"
    />

    <div>
      <Question
        v-if="!showResults"
        :question="quiz.questions[currentQuestionIndex]"
        @selectOption="onOptionSelected"
      />
      <Results 
        v-else
        :quizQuestionLength="quiz.questions.length"
        :numberofCorrectAnswers="numberofCorrectAnswers"
      />
    </div>

  </div>
  <Footer/>
</template>