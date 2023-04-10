<template>
  <div>
    <!-- main menu area  -->
    <b-container v-if="!mainMenu">
      <b-row>
        <b-col>
          <h1> Multiple Choice Quiz </h1>
        </b-col>
      </b-row>
      <b-row>
        <b-col>
          <b-button class="playButton" @click="mainMenu = true">START</b-button>
        </b-col>
        <b-col>
          <b-button class="howButton" @click="showHow = true">HELP</b-button>
        </b-col>
      </b-row>
    </b-container>
    <b-modal v-model="showHow" title="How to Play" hide-footer>
      <p> Choose the best answer in every question! </p>
    </b-modal>
    <!-- question area  -->
    <b-container v-if="mainMenu">
      <div v-if="!quizGame">
        <h3>{{currentQuestionNumber}} / {{questions.length}} {{ currentQuestion.question }}</h3>
        <div v-for="(answer, answerIndex) in currentQuestion.answers" :key="answerIndex">
          <b-button class="choiceButton" @click="checkAnswer(answer)">{{ answer.text }}</b-button>
        </div>
        <!-- modal correct/wrong area  -->
        <b-modal v-model="showAnswer" title="Answer" hide-footer hide-header-close  no-close-on-esc no-close-on-backdrop>
          <p v-if="isCorrectAnswer">Correct!</p>
          <p v-else>Incorrect!</p>
          <b-button @click="nextQuestion">Next</b-button>
        </b-modal>
      </div>
      <!-- modal score area -->
      <b-modal v-model="quizGame" title="Done!" hide-footer hide-header-close  no-close-on-esc no-close-on-backdrop >
        <p>Score: {{ score }} out of {{ questions.length }}</p>
        <b-button class="menuButton" @click="backMenu">Main Menu</b-button>
      </b-modal>
    </b-container>
  </div>
</template>

<script>
export default {
  data() {
    return {
      mainMenu: false,
      quizGame: false,
      showHow: false,
      showAnswer: false,
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
      currentQuestionIndex: 0,
      score: 0,
      selectedAnswer: null,
    };
  },
  computed: {
    currentQuestion() {
      return this.questions[this.currentQuestionIndex];
    },
    currentQuestionNumber () {
      return this.currentQuestionIndex + 1;
    },
    isCorrectAnswer() {
      const selectedAnswer = this.selectedAnswer;
      if (!selectedAnswer) {
        return false;
      }
      const correctAnswer = this.currentQuestion.answers.find(answer => answer.correct === true);
      return selectedAnswer === correctAnswer;
    }
  },
  methods: {
    checkAnswer(answer) {
      this.showAnswer = true;
      this.selectedAnswer = answer;
      if (answer.correct) {
        this.score++;
      }
    },
    nextQuestion() {
      this.showAnswer = false;
      this.selectedAnswer = null;
      if (this.currentQuestionIndex === this.questions.length - 1) {
        this.quizGame = true;
      } else {
        this.currentQuestionIndex++;

      }
    },
    backMenu () {
      this.mainMenu = false;
      this.quizGame = false;
      this.currentQuestionIndex = 0;
      this.score = 0;
      this.selectedAnswer = null;
    }
  }
};
</script>

<style>

</style>