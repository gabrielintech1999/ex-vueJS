<template>
    <div class="quote-generator">
      <h1>Random Quote Generator</h1>
      <p class="quote">{{ currentQuote }}</p>
      <button @click="generateRandomQuote">New Quote</button>
    </div>
  </template>
  
  <script setup>
  // Importando a função ref para lidar com reatividade
  import { ref } from 'vue';
  
  // Array de citações
  const quotes = [
    "The greatest glory in living lies not in never falling, but in rising every time we fall. - Nelson Mandela",
    "The way to get started is to quit talking and begin doing. - Walt Disney",
    "Your time is limited, so don't waste it living someone else's life. - Steve Jobs",
    "If life were predictable it would cease to be life, and be without flavor. - Eleanor Roosevelt",
    "If you look at what you have in life, you'll always have more. - Oprah Winfrey",
    "Life is what happens when you're busy making other plans. - John Lennon"
  ];
  
  // Definindo o estado reativo para a citação atual
  const currentQuote = ref(quotes[0]);
  
  // Função para gerar uma citação aleatória
  const generateRandomQuote = () => {
    const randomIndex = Math.floor(Math.random() * quotes.length);
    currentQuote.value = quotes[randomIndex];
  };
  </script>
  
  <style scoped>
  .quote-generator {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 100vh;
    background-color: #f0f0f0;
    font-family: 'Arial', sans-serif;
  }
  
  h1 {
    font-size: 2rem;
    margin-bottom: 20px;
  }
  
  .quote {
    font-size: 1.5rem;
    margin-bottom: 20px;
    padding: 0 20px;
    text-align: center;
  }
  
  button {
    padding: 10px 20px;
    font-size: 1rem;
    cursor: pointer;
    background-color: #4caf50;
    color: white;
    border: none;
    border-radius: 5px;
    transition: background-color 0.3s ease;
  }
  
  button:hover {
    background-color: #45a049;
  }
  </style>
  