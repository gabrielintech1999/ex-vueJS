<template>
  <div id="app">
    <h1>Site de Apostas</h1>

    <div class="games">
      <h2>Jogos Disponíveis</h2>
      <div v-for="game in games" :key="game.id" class="game">
        <h3>{{ game.name }}</h3>
        <p>Odds: {{ game.odds }}</p>
        <button @click="placeBet(game)">Fazer Aposta</button>
      </div>
    </div>

    <div class="betting" v-if="selectedGame">
      <h2>Aposta no jogo: {{ selectedGame.name }}</h2>
      <form @submit.prevent="submitBet">
        <label for="amount">Quantia:</label>
        <input type="number" v-model="betAmount" min="1" required />

        <button type="submit">Confirmar Aposta</button>
      </form>
    </div>

    <div class="bet-history">
      <h2>Histórico de Apostas</h2>
      <ul>
        <li v-for="(bet, index) in betHistory" :key="index">
          Jogo: {{ bet.game.name }} | Quantia: {{ bet.amount }} | Odds: {{ bet.game.odds }}
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const games = ref([
      { id: 1, name: "Time A vs Time B", odds: "2.5" },
      { id: 2, name: "Time C vs Time D", odds: "3.1" },
    ]);

    const selectedGame = ref(null);
    const betAmount = ref(null);
    const betHistory = ref([]);

    const placeBet = (game) => {
      selectedGame.value = game;
      betAmount.value = null;
    };

    const submitBet = () => {
      if (betAmount.value && selectedGame.value) {
        betHistory.value.push({
          game: selectedGame.value,
          amount: betAmount.value,
        });
        selectedGame.value = null;
        betAmount.value = null;
      }
    };

    return {
      games,
      selectedGame,
      betAmount,
      betHistory,
      placeBet,
      submitBet,
    };
  },
};
</script>

<style>
#app {
  font-family: 'Arial', sans-serif;
  padding: 20px;
}

.games, .bet-history {
  margin-bottom: 20px;
}

.game {
  margin-bottom: 10px;
}

button {
  margin-top: 10px;
  padding: 5px 10px;
}

form {
  margin-top: 10px;
}
</style>


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
