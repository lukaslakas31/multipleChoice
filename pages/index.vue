<template>
  <multipleChoice :questions="questions"/> 
  </template>
  
  <script>
    export default {
      data() {
        return {
          questions: [
        {
          question: "'OS' Computer abbreviation usually means?",
          answers: [
            { text: "Open Software", correct: false },
            { text: "Operating System", correct: true },
            { text: "Optical Sensor", correct: false },
          ]
        },
        {
          question: "How many bits is a byte?",
          answers: [
            { text: "4", correct: false },
            { text: "8", correct: true },
            { text: "16", correct: false },
          ]
        },
        // add questions
      ],
        }
    }
    }
  </script>
  
  <style>

  </style>