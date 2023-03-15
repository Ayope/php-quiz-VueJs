<template>
    <div>
      <Stepper  :state="state"/>
    </div>
    
    <main>
      <section v-if="page=='info'">
        <Info @StartQuiz="showQuiz"/>
      </section>
      
      <section v-if="page=='quiz'" class="quizz">
        <Quiz @return-score="showScore"/>
      </section>

      <section v-if="page=='score'">
        <Score :result="result"/>
      </section>
    </main>
</template>

<script>
import Info from './components/Info.vue'
import Quiz from './components/Quiz.vue'
import Stepper from './components/Stepper.vue'
import Score from './components/Score.vue'

export default {
  name: 'App',
  components:{
    Info,
    Quiz,
    Stepper,
    Score
  },

  data() {
    return {
      page: 'info',
      result: null,
      state: 'info'
    }
  },
  
  methods:{
    showInfo(){
      this.state = 'info'
      this.page = 'info'
    },
    showQuiz(){
      this.state = 'quiz'
      this.page = 'quiz'
    },
    showScore(result){
      this.state = 'score'
      this.result = result
      this.page = 'score' 
    }
    
  }
}
</script>

<style>
  body{
    display: grid;
    background-color: darkslategray;
    color: #fff;
    font-family: 'Montserrat', sans-serif;
  }

  main{
    margin-top: 30px;
    display: flex;
    height: 80vh;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    text-align: center;
  }

  .quizz{
    width: 60%;
  }

  @media (max-width: 600px) {
    .quizz {
      width: 90%;
    }
  }
</style>
