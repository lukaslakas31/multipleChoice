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
            { text: "Operating System", correct: true },
            { text: "Open Software", correct: false },
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
        {
          question: " Computers calculate numbers in what mode? ",
          answers: [
            { text: " Octal ", correct: false },
            { text: " Binary ", correct: true },
            { text: " Decimal ", correct: false },
          ]

        },
        {
          question: " http://www.indiabix.com - is an example of what? ",
          answers: [
            { text: " A Server ", correct: false },
            { text: " A Directory ", correct: false },
            { text: " A URL", correct: true },
          ]
        },
        {
          question: " 'DB' computer abbreviation usually means?  ",
          answers: [
            { text: " Database ", correct: true },
            { text: " Data Block ", correct: false },
            { text: " Driver Boot ", correct: false },
          ]
        },
        {
          question: " The speed of your net access is defined in terms of. ",
          answers: [
            { text: " RAM ", correct: false },
            { text: " MHz ", correct: false },
            { text: " Megabytes ", correct: true },
          ]

        },
        {
          question: " '.MOV' extension refers usually to what kind of file?   ",
          answers: [
            { text: " Audio File ", correct: false },
            { text: " Image File ", correct: false },
            { text: " Animation/Movie File ", correct: true },
          ]
        },
        {
          question: " What does CPU stand for? ",
          answers: [
            { text: " Computer Processing Unit  ", correct: false },
            { text: " Central Processing Unit ", correct: true },
            { text: " Core Processing Unit ", correct: false },
          ]
        },
        {
          question: " What do you call a computer on a network that requests files from another computer?  ",
          answers: [
            { text: " A client ", correct: true },
            { text: " A Host ", correct: false },
            { text: " A Router ", correct: false },
          ]
        },
        {
          question: " Which of the following is not a programming language? ",
          answers: [
            { text: " Python ", correct: false },
            { text: " Turing ", correct: true },
            { text: " Java ", correct: false },
          ]
        },
      ],
        }
    }
    }
  </script>
  
  <style>

  </style>