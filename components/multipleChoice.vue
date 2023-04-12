<template>
  <div class="content">
    <!-- main menu area  -->
    <div class="main" v-if="!mainMenu">
          <h1 id="title">
            <span class="quiz-text">Quiz</span>Dom
          </h1>
          <b-button class="playButton" @click="mainMenu = true">START</b-button>
          <b-button class="howButton" @click="showHow = true">HELP</b-button>
    </div>
    <b-modal v-model="showHow" title="How to Play" ok-only centered size="m" header-bg-variant="dark" header-text-variant="light"  body-bg-variant="dark" body-text-variant="light" footer-bg-variant="dark" footer-text-variant="light">
      <p id="howGame"> Choose the best answer in every question! </p>
    </b-modal>


    <!-- question area  -->
    <div class="question" v-if="mainMenu">
      <div class="questionpart" v-if="!quizGame">
        <div class="tops">
          <h3 class="qnum">{{currentQuestionNumber}} / {{questions.length}} </h3>
          
          <p class="timer">{{ timeLeft }}<i class="fa-solid fa-clock"></i></p>
        </div>
          <div class="qanda">
              <h3 class="quest">{{ currentQuestion.question }}</h3>
              <div class="choices">
                <div v-for="(answer, answerIndex) in currentQuestion.answers" :key="answerIndex">
                  <b-button class="choiceButton" :class="'answer'+answerIndex" :id="answerIndex" @click="checkAnswer(answerIndex)">{{ answer.text }}</b-button>
                </div>
              <!-- modal correct/wrong area  -->
              <b-modal class="result" v-model="showAnswer" title="Answer" hide-footer hide-header-close no-close-on-esc no-close-on-backdrop size="lg" centered header-bg-variant="dark" header-text-variant="light"  body-bg-variant="dark" body-text-variant="light">
                <div class="ansResult">
                  <p v-if="this.isCorrect">Correct!<br><i class="fa-solid fa-square-check" id="corIcon" style="color: #13cd1f;"></i></p>
                  <p v-else-if="!this.isCorrect">Incorrect!<br><i class="fa-solid fa-square-xmark" id="wroIcon" style="color: #e33131;"></i></p>
                  <b-button @click="nextQuestion">Next Question</b-button>
                </div>
              </b-modal>
          </div>
        </div>
      </div>
      <!-- modal score area -->
      <b-modal v-model="quizGame" title="Done!" hide-footer hide-header-close  no-close-on-esc no-close-on-backdrop centered header-bg-variant="dark" header-text-variant="light"  body-bg-variant="dark" body-text-variant="light" >
        <p>Score: {{ score }} out of {{ questions.length }}</p>
        <b-button class="menuButton" @click="backMenu">Main Menu</b-button>
      </b-modal>
    </div>
  </div>
</template>


<script>
export default {
  props:['questions'],
  data() {
    return {
      mainMenu: false,
      quizGame: false,
      showHow: false,
      showAnswer: false,
      currentQuestionIndex: 0,
      score: 0,
      selectedAnswer: null,
      timeLeft: 10,
      isCorrect: false,
    };
  },
  watch: {
    mainMenu: {
      handler() {
        if (this.mainMenu) {
          this.startTimer();
        } else {
          this.stopTimer();
        }
      },
      immediate: true,
    }
  },
  computed: {
    currentQuestion() {
      return this.questions[this.currentQuestionIndex];
    },
    currentQuestionNumber () {
      return this.currentQuestionIndex + 1;
    },

  },
  methods: {
    startTimer() {
      this.timerId = setInterval(() => {
        if (this.timeLeft === 0) {
            this.timesUp();
            clearInterval(this.timerId);
            return;
      }
      if(!this.mainMenu) {
        clearInterval(this.timerId);
        return;
      }
      this.timeLeft--;
      }, 1000);
    },
    timesUp() {
      this.showAnswer = true;
      this.isCorrect = false;
      this.stopTimer();
    },
    stopTimer() {
      clearInterval(this.timerId);
    },
    checkAnswer(answerID) {
      if (this.timeLeft === 0 ){
        this.timesUp();
        return;
      }
      this.isCorrect = this.questions[this.currentQuestionIndex].answers[answerID].correct;
      this.showAnswer = true;
      if (this.isCorrect) {
        this.score++;
      }
      this.stopTimer();
    },
    nextQuestion() {
      this.stopTimer();
      this.showAnswer = false;
      this.selectedAnswer = null;
      if (this.currentQuestionIndex === this.questions.length - 1) {
        this.quizGame = true;
      } else {
        this.currentQuestionIndex++;
        this.timeLeft = 10;
        this.startTimer();
      }
    },
    backMenu () {
      this.mainMenu = false;
      this.quizGame = false;
      this.currentQuestionIndex = 0;
      this.score = 0;
      this.selectedAnswer = null;
      this.stopTimer();
      clearInterval(this.timerId);
      this.showAnswer = false;
      this.timeLeft = 10;
      this.startTimer();
    }
  }
};
</script>

<style>
  html, body {
  height: 100%;
  margin: 0;
  padding: 0;
  background-color: #461a42;
}

.main{
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 100%;
  display: flex;
  min-height: 100vh;
  margin: 0;
  padding: 0;
  gap: 80px;
}

#title {
  font-family: cursive;
  font-weight: 400;
  font-size: 150px;
  color: #eca82c;
  text-align: center;
  line-height: 0.8;
}

  .quiz-text {
    color: #FFFFFF;
  }

  .playButton{
    color: white;
    background-color: rgb(21, 199, 113);
    font-size: 30px;
    border-radius: 15px;
    box-shadow: 0px 17px 0px 0px rgb(77, 115, 138);
    border: none;
    padding: 5px 25px;
    cursor: pointer;
    letter-spacing: 3px;
  }

  .playButton:hover{
    background-color: rgb(14, 169, 94);
  }

  .playButton:active{
    transform: translateY(7px);
    box-shadow: 0px 10px 0px 0px rgb(67, 88, 93);
  }
  .howButton{
    color: white;
    background-color: #474E68;
    font-size: 30px;
    border-radius: 15px;
    box-shadow: 0px 17px 0px 0px rgb(77, 115, 138);
    border: none;
    padding: 5px 25px;
    cursor: pointer;
    letter-spacing: 3px;
  }

  .howButton:hover{
    background-color: #404258;
  }

  .howButton:active{
    transform: translateY(7px);
    box-shadow: 0px 10px 0px 0px rgb(67, 88, 93);
  }

  .modal-header{
    justify-content: center;
  }

  .modal-header h5{
    font-size: 40px;
  }

  button.close.text-light{
    display: none;
  }
  
  #howGame {
    text-align: center;
  }

  .btn-primary {
    color: #fff;
    background-color: #474E68;
    border-color: #fff;
  }

  .btn-primary:hover{
    background-color: #474E68;
    border-color: #fff;
  }

  .timer{
    color:#FFFFFF;
    font-size: 40px;
  }

  .question{
    min-height: 100vh;
    margin: 0;
    padding: 0;
    display: flex;
    flex-direction: column;
    align-content: space-between;
  }

  .tops{
    display: flex;
    justify-content: space-between;
    margin: 15px;
  }

  .qnum{
    color:#FFFFFF;
    font-size: 40px;
  }

  .timer i{
    font-size: 30px;
    border: solid #FFFFFF;
    border-radius: 50%;
    margin-left: 10px;
    margin-top: 5px;
  }

  .quest{
    display: flex;
    justify-content: center;
    color: #FFFFFF;
    font-size: 50px;
  }

  .qanda{
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    min-height: 85vh;
    gap: 100px;
  }

  .qanda .choices{
    display: flex;
    flex-direction: row;
    justify-content: space-around;
    width: 100%;
    margin-top: 100px;
  }
 
  .choiceButton{
    font-size: 50px;
    width: 600px;
    height: 400px;
  }
  .choiceButton.answer0 {
   background-color: #FFA500; /* set background color for choice 0 */
  }
  .choiceButton.answer1 {
   background-color: #6495ED; /* set background color for choice 1 */
  }
  .choiceButton.answer2 {
   background-color: #FF69B4; /* set background color for choice 2 */
  }

  .ansResult{
    display: flex;
    flex-direction: column;
    align-items: center;
    font-size: 50px;
    gap: 90px;
  }

  .ansResult p{
    margin-top: 60px;
  }

  #corIcon{
    font-size: 80px;
    margin-left: 50px;
    border: none;
  }

  #wroIcon{
    font-size: 80px;
    margin-left: 70px;
    border: none;
  }

  .modal-body{
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 50px;
  }

  .modal-body p{
    font-size: 50px;
    font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
  }
</style>