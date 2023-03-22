<script setup>
    import q from "../data/quizes.json"
    import {ref, watch} from "vue"
    import Card from "../components/Card.vue"
    import Footer from "../components/Footer.vue" 
  
    const quizes = ref(q)
    const search = ref("")
    const searchEmpty = ref(false)

    watch(search, () => {
      quizes.value = q.filter(quiz => quiz.name.toLowerCase().includes(search.value.toLowerCase()))

      if (quizes.value.length < 1){
        searchEmpty.value = true;
      }
      else{
        searchEmpty.value = false;
      }
    })
  
  ;
  </script>
  
  <template>
    <div>
      <header>
        <h1>Quizes</h1>
        <input v-model.trim="search" type="text" placeholder="Search...">
      </header>
      <div class="options-container">
        <div v-if="searchEmpty">
          <p>Try searching something else. No results found.</p>
        </div>
        <Card v-else v-for="(quiz, index) in quizes" :key="quiz.id" :quiz="quiz" :data-index="index" />
      </div>
    </div>
    <Footer/>
  </template>
  
  <style scoped>
    p {
      font-size: 25px;
    }
  
    header {
      margin-bottom: 10px;
      margin-top: 30px;
      display: flex;
      align-items: center;
    }
  
    header h1 {
      font-weight: bold;
      margin-right: 30px;
    }
  
    header input {
      border: none;
      background-color: rgba(128,128,128,0.1);
      padding: 10px;
      border-radius: 5px;
    }
  
    .options-container {
      display: flex;
      flex-wrap: wrap;
      margin-top: 40px;
    }
    
  </style>