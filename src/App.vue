<template>
  <div class="container">
    <Component :is="screens[position]" 
    :question="question" 
    :result="result" 
    @goto='handleGoTo'
    @question='handleQuestion'
    @startOver='startOver'
    @showResult='showResult' />
  </div>

</template>

<script>
import appInitial from './components/initial.vue'
import appConform from './components/conform-app.vue'
import appResults from './components/results.vue'

export default {
  components: {
    appInitial,
    appConform,
    appResults
  },
  data() {
    return {
      list: ["Yes", "No", "Maybe", "Not sure..try again", "Ask a friend", "Call the police",],
      screens: ['appInitial', 'appConform', 'appResults'],
      position: 0,
      question: '',
      result: ''
    }
  },
  methods: {
    handleGoTo(position) {
      this.position = position;
    },
    handleQuestion(question) {
      this.question = question;
    },
    getRandomValue() {
      return this.list[Math.floor(Math.random() * this.list.length)]

    },
     generateResult() {
      let rand = this.getRandomValue();
      if(this.result !== ''){
          while (rand === this.result){
            rand = this.getRandomValue();
          }
      }
      this.result = rand;
      console.log(this.result);
    },
    showResult() {
      this.generateResult()

    },
    startOver(){
      this.position= 0,
      this.question= '',
      this.result= ''
    }
  }
}

</script>

<style>
@import './assets/style.css'
</style>
