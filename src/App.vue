<template>
  <div id="app"> 
     <Header 
     :numCorrect = "numCorrect"
     :numTotal = "numTotal"
     /> 
     <b-container class="bv-example-row">
      <b-row>
        <b-col sm="6" offset="3">
             <QuestionBox 
              v-if="questions.length" 
              :currentQuestion="questions[index]"
              :next="next"
              :increment="increment"
              /> 
        </b-col> 
      </b-row>
  </b-container> 
  </div>
</template>

<script>
 import Header from './components/Header.vue'
 import QuestionBox from './components/QuestionBox.vue'

export default {
  name: 'App',
  components: {
  Header,
  QuestionBox
  },
  data() {
    return {
       questions: [],
       index: 0, 
       numCorrect: 0,
       numTotal: 0
    }
  },
  // Methods to increment index value, in order to navigate through questions
  methods:{
  next() {
    this.index++
  }
  },
    increment(isCorrect){
    // keep truck of two things: Total user sumbssion Answer, And total number of correct answer
    if(isCorrect)
    {
        this.numCorrect++
    }
    this.numTotal++
    // Make sure you pass the 2 value in the haider component.
  },
  mounted: function(){
    // mounted hook used lifecycle hook in vue, Vue calls the mounted() hook when component is added to the DOM
    // Often used to send an Http request to fetch data tha the component will render
    fetch('https://opentdb.com/api.php?amount=10&category=19&type=multiple', {
      method: 'get'
    })
    //Taking the response
    .then ((response) => {
    return response.json()
    })
    .then((jsonData) => {
    // Accessing data for the application
    this.questions = jsonData.results
    })
  }


}
</script>

<style>
 

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing:grayscale;
 text-align: center;
  color: brown;
  margin-top:60px;
}
</style>
