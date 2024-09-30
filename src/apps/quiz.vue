<template>
    <div class="quiz-app">
        <h1>Quiz App</h1>
        <div v-if="currentQuestionIndex < questions.length">
            <h2>{{ currentQuestionIndex + 1 }}. {{ currentQuestion.question }}</h2>
            <ul>
                <li v-for="(answer, index) in currentQuestion.answers" :key="index">
                    <button @click="checkAnswer(answer)">{{ answer.text }}</button>
                </li>
            </ul>
            <div v-if="feedback" class="feedback">{{ feedback }}</div>
        </div>
        <div v-else>
            <h2>Fim do questionário!</h2>
            <p>Você respondeu {{ score }} de {{ questions.length }} perguntas corretamente.</p>
            <button @click="restartQuiz">Reiniciar Quiz</button>
        </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
        return {
            questions: [
                {
                    question: "Qual é a capital da França?",
                    answers: [
                        { text: "Paris", correct: true },
                        { text: "Londres", correct: false },
                        { text: "Roma", correct: false },
                        { text: "Berlim", correct: false }
                    ]
                },
                {
                    question: "Qual é o maior planeta do sistema solar?",
                    answers: [
                        { text: "Terra", correct: false },
                        { text: "Marte", correct: false },
                        { text: "Júpiter", correct: true },
                        { text: "Saturno", correct: false }
                    ]
                },
                {
                    question: "Quem escreveu 'Dom Casmurro'?",
                    answers: [
                        { text: "Machado de Assis", correct: true },
                        { text: "José de Alencar", correct: false },
                        { text: "Clarice Lispector", correct: false },
                        { text: "Jorge Amado", correct: false }
                    ]
                }
            ],
            currentQuestionIndex: 0,
            score: 0,
            feedback: ""
        };
    },
    computed: {
        currentQuestion() {
            return this.questions[this.currentQuestionIndex];
        }
    },
    methods: {
        checkAnswer(answer) {
            if (answer.correct) {
                this.score++;
                this.feedback = "Correto!";
            } else {
                this.feedback = "Incorreto!";
            }
            this.currentQuestionIndex++;
            setTimeout(() => {
                this.feedback = "";
            }, 2000);
        },
        restartQuiz() {
            this.currentQuestionIndex = 0;
            this.score = 0;
            this.feedback = "";
        }
    }
  };
  </script>
  
  <style>
  .quiz-app {
    max-width: 600px;
    margin: auto;
    text-align: center;
  }
  
  .feedback {
    margin-top: 10px;
    font-weight: bold;
  }
  </style>