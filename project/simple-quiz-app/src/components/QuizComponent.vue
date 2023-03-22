<template>
  <main class="app">
    <h1>The Quiz</h1>

    <section class="quiz" v-if="!quizCompleted">
      <div class="quiz-info">
        <span class="question"
          >{{ this.currentQuestion + 1 }}.
          {{ getCurrentQuestion.question }}</span
        >
        <span class="score">Score {{ score }}/{{ questions.length }}</span>
      </div>

      <div class="options">
        <label
          v-for="(option, index) in getCurrentQuestion.options"
          :key="index"
          :for="'option' + index"
          :class="`option ${
            getCurrentQuestion.selected == index
              ? index == getCurrentQuestion.answer
                ? 'correct'
                : 'wrong'
              : ''
          } ${
            getCurrentQuestion.selected != null &&
            index != getCurrentQuestion.selected
              ? 'disabled'
              : ''
          }`"
        >
          <input
            type="radio"
            :id="'option' + index"
            :name="getCurrentQuestion.index"
            :value="index"
            v-model="getCurrentQuestion.selected"
            :disabled="getCurrentQuestion.selected"
            @change="setAnswer"
          />
          <span>{{ option }}</span>
        </label>
      </div>

      <button @click="nextQuestion" :disabled="!getCurrentQuestion.selected">
        {{
          getCurrentQuestion.index == questions.length - 1
            ? "Finish"
            : getCurrentQuestion.selected == null
            ? "Select an option"
            : "Next question"
        }}
      </button>
    </section>

    <section v-else>
      <h2>You have finished the quiz!</h2>
      <p>Your score is {{ score }}/{{ questions.length }}</p>
      <br /><br />
      <div style="text-align: center">
        <button @click="doItAgain">Do it again</button>
      </div>
    </section>
  </main>
</template>

<script>
export default {
  name: "QuizComponent",
  data() {
    return {
      questions: [
        {
          question: "What is Vue?",
          answer: 0,
          options: ["A framework", "A library", "A type of hat"],
          selected: null,
        },
        {
          question: "What is Vuex used for?",
          answer: 2,
          options: [
            "Eating a delicious snack",
            "Viewing things",
            "State management",
          ],
          selected: null,
        },
        {
          question: "What is Vue Router?",
          answer: 1,
          options: [
            "An ice cream maker",
            "A routing library for Vue",
            "Burger sauce",
          ],
          selected: null,
        },
        {
          question: "Why is Vue.js called a progressive framework?",
          answer: 0,
          options: [
            "Vue.js is called a progressive framework because it is being changed and developed continually.",
            "Vue.js is called a progressive framework because it facilitates us to create Dynamic User Interfaces and single-page applications",
            "Vue.js is called a progressive framework because it follows the latest JavaScript standards.",
            "All of the above.",
          ],
          selected: null,
        },
        {
          question: "Which company invented Vue.js?",
          answer: 1,
          options: ["Facebook", "Google", "Oracle", "Twitter"],
          selected: null,
        },
        {
          question:
            "Which of the following data binding interpolation is also known as 'Mustache' syntax?",
          answer: 2,
          options: ["v-on", "v-model", "{{ }}", "[]"],
          selected: null,
        },
        {
          question:
            "Which of the following is the correct way to install Vue.js in your project?",
          answer: 3,
          options: [
            "We can install Vue.js by using CDN by including <script> tag in HTML file.",
            "We can install Vue.js by using Node Package Manager (NPM)",
            "You can install Vue.js using Bower.",
            "All of the above.",
          ],
          selected: null,
        },
        {
          question:
            "Which of the following event modifier should we use to perform the click event only for the one time?",
          answer: 1,
          options: [
            "<a @:click.passive='dotask'></a>",
            "<a @:click.once='dotask'></a>",
            "<a @:click.prevent-once='dotask'></a>",
            "<a @:click.prevent-once='dotask'></a>",
          ],
          selected: null,
        },
        {
          question: "How many types of directives are available in Vue.js?",
          answer: 2,
          options: ["2", "3", "4", "5"],
          selected: null,
        },
        {
          question:
            "Which of the following is a core feature of Mixins in Vue.js?",
          answer: 3,
          options: [
            "Mixins provide great flexibility.",
            "Mixin contains options for Vue.js components. You can use Mixins in Vue.js safely because they do not affect changes outside their defined scope.",
            "Mixins in Vue.js provide a great platform for code reusability.",
            "All of the above.",
          ],
          selected: null,
        },
      ],
      quizCompleted: false,
      currentQuestion: 0,
    };
  },
  methods: {
    setAnswer(e) {
      this.questions[this.currentQuestion].selected = e.target.value;
      e.target.value = null;
    },
    nextQuestion() {
      if (this.currentQuestion < this.questions.length - 1) {
        this.currentQuestion++;
        return;
      }
      this.quizCompleted = true;
    },
    doItAgain() {
      window.location.reload();
    },
  },
  computed: {
    getCurrentQuestion() {
      let question = this.questions[this.currentQuestion];
      question.index = this.currentQuestion;
      return question;
    },
    score() {
      let value = 0;
      this.questions.map((q) => {
        if (q.selected !== null && q.answer == q.selected) {
          console.log("Correct");
          value++;
        }
      });
      return value;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
