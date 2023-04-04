<template>
    <div class="container"> 
        <h1> Quiz<span>dom</span></h1>
        <div>
        <b-button @click="startQuiz">Start</b-button>
        <b-button @click="showHelp">Help</b-button>
        <div v-if="helpVisible" class="help-box">
            <p> How to Play: </p>
            <ul>
            <li>Read the questions carefully</li>
            <li>Click the best answer of the question</li>
            <li>Repeat until you've answered all the questions</li>
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