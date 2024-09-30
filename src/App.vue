<template>
  <div class="quiz-app">
    <div v-if="currentQuestionIndex < questions.length">
      <h1>Quiz App</h1>
      <h1>{{ currentQuestionIndex + 1 }}. {{ currentQuestion.question }}</h1>
      <ol type="a">
        <li v-for="(answer, i) in currentQuestion.answers" :key="i">
          <button @click="checkAnswer(answer)">{{ answer.text }}</button>
        </li>
      </ol>
      <h1 v-if="feedback" >{{ feedback }}</h1>
    </div>

    <div v-else>
      <h1>Fim do jogo</h1>
      <ul>
        <li>Pontuacao final: {{score}}</li>
        <li>Total de perguntas: {{questions.length}}</li>
      </ul>
      <button @click="resetQuiz">Jogar Novamente</button>
    </div>
  </div>
</template>

<script setup>
import { computed, ref } from "vue";

const score = ref(0);
const feedback = ref();

const questions = ref([
  {
    question: "Qual é a capital da França?",
    answers: [
      { text: "Paris", correct: true },
      { text: "Londres", correct: false },
      { text: "Roma", correct: false },
      { text: "Berlim", correct: false },
    ],
  },
  {
    question: "Qual é o maior planeta do sistema solar?",
    answers: [
      { text: "Terra", correct: false },
      { text: "Marte", correct: false },
      { text: "Júpiter", correct: true },
      { text: "Saturno", correct: false },
    ],
  },
  {
    question: "Quem escreveu 'Dom Casmurro'?",
    answers: [
      { text: "Machado de Assis", correct: true },
      { text: "José de Alencar", correct: false },
      { text: "Clarice Lispector", correct: false },
      { text: "Jorge Amado", correct: false },
    ],
  },
]);

const currentQuestionIndex = ref(0);

const currentQuestion = computed(() => {
  return questions.value[currentQuestionIndex.value];
});

const checkAnswer = (answer) => {
  if (answer.correct) {
    score.value++;
    feedback.value = "Correcto";
    
  } else {
    feedback.value = "Incorrecto";
  }

  currentQuestionIndex.value++;

  setTimeout(() => {
    feedback.value = ""
  }, 2000);

};

const resetQuiz = () => {
  currentQuestionIndex.value = 0;
  score.value = 0;

};
</script>

<!-- <script setup>
  import { ref } from "vue";

  const newValue = ref("")

  console.log(newValue.value);
  

  async function getData() {

    const apiKey = "be7333a154937ee1b9131c3cf5221405"
    const res = await fetch(`https://api.openweathermap.org/data/2.5/weather?q=${"Angola"}&appid=${apiKey}`)

    const data = await res.json()

    console.log(data);
    
  }

  getData()

</script>

<template>
  <input type="text" v-model="newValue">
  <h1 v-if="newValue">{{ newValue }}</h1>
  <h1>Hello App weather</h1>
</template> -->

<!-- <script setup lang="ts">
import HelloWorld from './components/HelloWorld.vue'
</script>

<template>
  <div>
    <a href="https://vitejs.dev" target="_blank">
      <img src="/vite.svg" class="logo" alt="Vite logo" />
    </a>
    <a href="https://vuejs.org/" target="_blank">
      <img src="./assets/vue.svg" class="logo vue" alt="Vue logo" />
    </a>
  </div>
  <HelloWorld msg="Vite + Vue" />
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style> -->
