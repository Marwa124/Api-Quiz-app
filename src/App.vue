<template>
  <div id="app">
    <router-link to="/">Home</router-link>
    <app-header :numCorrect="numCorrect" :numTotal="numTotal"></app-header>
    <b-container class="bv-example-row">
      <b-row>
        <b-col sm="6" offset-md="3">
          <!-- <component
            :is="component = 'question-box'"
            v-if="jsonQuestions.length"
            :currentQuestion="jsonQuestions[index]"
            :next="next"
            :increment="increment"
          /> -->
          <question-box
            v-if="jsonQuestions.length"
            :currentQuestion="jsonQuestions[index]"
            :next="next"
            :increment="increment"
          >
          </question-box>
        </b-col>
      </b-row>
    </b-container>
    <router-view />
  </div>
</template>

<script>
import AppHeader from "@/components/AppHeader";
import QuestionBox from "@/components/QuestionBox";

export default {
  name: "App",
  components: {
    AppHeader,
    QuestionBox
  },
  data: function() {
    return {
      jsonQuestions: [],
      index: 0,
      numCorrect: 0,
      numTotal: 0
    };
  },
  methods: {
    next: function() {
      this.index++;
    },
    increment(isCorrect) {
      if (isCorrect) {
        this.numCorrect++;
      }
      this.numTotal++;
    }
  },
  mounted: function() {
    fetch(
      "https://opentdb.com/api.php?amount=10&category=19&difficulty=medium&type=multiple",
      {
        method: "get"
      }
    )
      .then(response => response.json())
      .then(json => (this.jsonQuestions = json.results));
  }
};
</script>

<style lang="scss">
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
