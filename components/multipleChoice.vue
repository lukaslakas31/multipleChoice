<template>
    <div class="container"> 
        <h1> Quiz<span>dom</span></h1>
        <div>
        <button @click="startQuiz">Start</button>
        <button @click="showHelp">Help</button>
        <div v-if="helpVisible" class="help-box">
            <p> How to Play: </p>
            <ul>
            <li>Select an answer from the options provided</li>
            <li>Click the "Next" button to move to the next question</li>
            <li>Repeat until you've answered all the questions</li>
            <li>Click the "Submit" button to see your score</li>
          </ul>
        </div>
      </div>
    </div>
    </template>
    
    <script>
    export default {
      data() {
        return {
          helpVisible: false
        }
      },
      methods: {
        startQuiz() {
          this.$router.push('/questionPage')
        },
        showHelp() {
          this.helpVisible = !this.helpVisible
        }
      }
    }
    </script>
    
    <style>
    body{
      background-color: #461a42;
    }
    
    .container{
      border-style: solid;
      border-color: red;
      align-content: center;
      width: 100vw;
    }
    
    h1{
      font-family: ;
      text-align: center;
    }
    </style>