<template>
    <div class="question-box-container">
           <b-jumbotron> 
               <template v-slot:lead>
               {{currentQuestion.question}}
               </template> 
               <hr class="my-4"> 
               <b-list-group>
                    <b-list-group-item
                    v-for="(answer, index) in answers"
                    :key="index"
                    @click="selectAnswer(index)"
                    :class="[selectedIndex === index ? 'selected': '']" 
                    >
                    {{ answer }}
                    </b-list-group-item>
                </b-list-group>    
               
               <b-button 
               variant="primary" 
               @click="submitAnswer"
               >Submit</b-button>
               <b-button @click="next" variant="success" href="#">Next

               </b-button> 
          </b-jumbotron>
   </div>
</template>

<script>
/*  import _ from 'lodash' */
//object
export default{
     // In order to display current Question you have to refference it in Pops Object
    props: {
         currentQuestion: Object,
         next: Function,
         increment: Function
    },
    //function
    data(){
        return {
           selectedIndex: null,
            /* shuffleAnswers: [], */
            
             

        } 
    },
    computed: {
       answers(){
         let answers = [...this.currentQuestion.incorrect_answers]  
         answers.push(this.currentQuestion.correct_answer)
         return answers  
       }  
    },
    // To shufle the answer Methods
    watch: {
         currentQuestion(){
             this.selectedIndex = null
             /* this.shuffleAnswers() */
         } 
    },
    methods: {
      selectAnswer(index) {
           this.selectedIndex = index 
      },
      submitAnswer(){
         let isCorrect = false
          
         if(this.selectedIndex === this.correctIndex)
         {
              isCorrect = true
         }

         this.increment(isCorrect)
      }
     /*  shuffleAnswers() {
         let answers = [...this.currentQuestion.incorrect_answers, this.currentQuestion.correct_answer]
          shuffle(answers)  
      },  
      shuffle(array){
          var currentIndex = array.length, temporaryValue, randomIndex;

          //The remain element to shoufle
          while(0 !== currentIndex)
          {
               //Pick a remain element 
               randomIndex = Math.floor(Math.random() * currentIndex);
               currentIndex -= 1;

               // swap with current element.
               temporaryValue = array[currentIndex];
               array[currentIndex] = array[randomIndex];
               array[randomIndex] = temporaryValue;
          }
          return array;
     } */
      
      
    }
  

}
</script>

<style scoped>
.list-group{
     margin-bottom: 15px;

}
.list-group-item:hover{
     background: darkorange;
     cursor: pointer;

}
.btn {
     margin: 0 5px;
}
.selected{
     background-color: lightseagreen;
}
.correct {
     background-color:forestgreen;
}
.incorrect{
     background-color: red;
}
</style>