<template>
  <div class="question-container">
    <div>
      <b-jumbotron>
        <template v-slot:lead>{{ currentQuestion.question }} </template>
        <hr class="my-4" />
        <b-list-group v-for="(answer, index) in shuffledAnswers" :key="index">
          <b-list-group-item
            @click="selectedAnswer(index)"
            :class="answerClass(index)"
          >{{ answer }}</b-list-group-item>
        </b-list-group>

        <b-button variant="primary" @click="submitAnswer" :disabled="selectedIndex === null || answered">Submit</b-button>
        <b-button variant="success" @click="next" href="#">Next</b-button>
      </b-jumbotron>
    </div>
  </div>
</template>

<script>
import _ from "lodash";

export default {
  props: {
    currentQuestion: {
      type: Array
    },
    next: {
      type: Function
    },
    increment: Function
  },
  data() {
    return {
      selectedIndex: null,
      correctIndex: null,
      answered: false,
      shuffledAnswers: []
    };
  },
  methods: {
    selectedAnswer(index) {
      this.selectedIndex = index;
    },
    shuffleAnswer() {
      let answers = [
        ...this.currentQuestion.incorrect_answers,
        this.currentQuestion.correct_answer
      ];
      this.shuffledAnswers = _.shuffle(answers);
      this.correctIndex = this.shuffledAnswers.indexOf(this.currentQuestion.correct_answer);
    },
    submitAnswer() {
      let isCorrect = false;

      if (this.selectedIndex === this.correctIndex) {
        isCorrect = true;
      }
      this.answered = true;
      this.increment(isCorrect);
    },
    answerClass(index) {
      let answerClass = '';

      if(!this.answered && (this.selectedIndex === index)) {
        answerClass = 'selected';
      }else if(this.answered && (this.correctIndex === index)) {
        answerClass = 'correct'
      }else if(this.answered && (this.selectedIndex === index) && (this.correctIndex !== index)) {
        answerClass = 'incorrect'
      }

      return answerClass;
    }
  },
  watch: {
    currentQuestion: {
      immediate: true,
      handler() {
        this.selectedIndex = null;
        this.answered = false;
        this.shuffleAnswer();
      }
    }
  }
};
</script>

<style lang="scss" scoped>
.list-group-item {
  &:hover {
    background-color: rgba(blue, 0.3);
    cursor: pointer;
  }
}
a {
  margin: 15px 5px;
}
.selected {
  background-color: rgba(blue, 0.3);
}
.correct{
    background-color: rgba(green, .4)
}
.incorrect{
    background-color: rgba(red, .4)
}
</style>