<script setup>
  const { questionStatus, 
          quizQuestionLength 
        } = defineProps(['questionStatus','barPercentage']);
;
</script>

<template>
  <header>
      <h1>Question {{ questionStatus }}</h1>
      <div class="bar">
        <div class="completion" :style="{width: barPercentage}"></div>
      </div>
    </header>
</template>

<style scoped>
    header {
        margin-top: 20px
    }
    header h4 {
        font-size: 30px;
    }
    .bar {
        width: 300px;
        height: 50px;
        border: 3px solid #41b883 
    }
    .completion {
        height: 100%;
        background-color: #41b883;
    }
</style>
