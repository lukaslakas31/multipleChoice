<template>
  <div>
    <b-container v-if="!mainMenu">
      <b-row>
        <b-col>
          <H1> Multiple Choice Quiz </H1>
        </b-col>
      </b-row>
      <b-row>
        <b-col>
          <b-button @click="mainMenu = true">Play</b-button>
        </b-col>
        <b-col>
          <b-button @click="showHow = true">How</b-button>
        </b-col>
      </b-row>
    </b-container>
    <b-modal v-model="showHow" title="How to Play" hide-footer>
      <p> Choose the best answer in every question! </p>
    </b-modal>
    <b-container v-if="mainMenu">
      <div v-if="!showScore">
        <h3>{{currentQuestionNumber}} / {{questions.length}} {{ currentQuestion.question }}</h3>
        <div v-for="(answer, answerIndex) in currentQuestion.answers" :key="answerIndex">
          <b-button @click="checkAnswer(answer)">{{ answer.text }}</b-button>
        </div>
        <b-modal v-model="showAnswer" title="Answer" hide-footer hide-header-close  no-close-on-esc no-close-on-backdrop>
          <p v-if="isCorrectAnswer">Correct!</p>
          <p v-else>Incorrect!</p>
          <b-button @click="nextQuestion">Next</b-button>
        </b-modal>
      </div>
      <b-modal v-model="showScore" title="Score" hide-footer >
        <p>You got {{ score }} out of {{ questions.length }} questions correct!</p>
      </b-modal>
    </b-container>
  </div>
</template>

<script>
export default {
  data() {
    return {
      mainMenu: false,
      showHow: false,
      showAnswer: false,
      questions: [
        {
          question: "'OS' Computer abbreviation usually means?",
          answers: [
            { text: "Open Software", correct: false },
            { text: "Operating System", correct: true },
            { text: "Optical Sensor", correct: false },
            { text: "Order Significance", correct: false }
          ]
        },
        {
          question: "How many bits is a byte?",
          answers: [
            { text: "4", correct: false },
            { text: "8", correct: true },
            { text: "16", correct: false },
            { text: "32", correct: false }
          ]
        }
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
        this.showScore = true;
      } else {
        this.currentQuestionIndex++;

      }
    }
  }
};
</script>

<style>

</style>