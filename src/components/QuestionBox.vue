<template>
    <div class="question-box-container">
           <b-jumbotron> 
               <template v-slot:lead>
               {{currentQuestion.question}}
               </template> 
               <hr class="my-4"> 
               <p>
                  Answers here:
               </p> 
               <b-button variant="primary" href="#">Submit</b-button>
               <b-button variant="success" href="#">Next</b-button> 
          </b-jumbotron>
   </div>
</template>

<script>
//object
export default{
     // In order to display current Question you have to refference it in Pops Object
    props: {
         currentQuestion: Object
    } 
}
</script>