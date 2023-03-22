<script setup>
import {RouterLink} from "vue-router" 
import errorImage from "../assets/images/DrawKit Larry Character Illustration (4).svg"
import Footer from "../components/Footer.vue" 

</script>

<template>
  <div class="container">
    <div class="text_container">
      <h1>Error 404</h1>
      <p>Page not found</p>
      <RouterLink class="buttonGoBack" to="/">Go back</RouterLink>
    </div>
    <div class="img_container">
      <img class="error_img" :src="errorImage">
    </div>
  </div>
  <Footer/>
</template>

<style scoped>
  .container {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: center;
    margin-top: 10%;
  }
  .text_container {
      flex: 1;
      text-align: center;
    }
  .img_container {
    flex: 1;
  }

  h1 {
    font-size: 80px;
  }
  p {
    font-size: 25px;
    margin-bottom: 20px;
  }
  .error_img{
    transform: scaleX(-1);
  }
  .buttonGoBack {
    font-size: 20px;
    text-decoration: none;
    border-radius: 50px;
    color: white;
    margin-top: 20px;
    padding: 10px 20px ;
    background-color: var(--color-text)
  }
</style>