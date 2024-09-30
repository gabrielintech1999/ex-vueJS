<template>
  <div id="app">
    <h1>Habit Tracker</h1>
    <div>
      <input v-model="newHabit" placeholder="Adicionar novo hábito" />
      <button @click="addHabit">Adicionar</button>
    </div>

    <div class="habits-list">
      <h2>Meus Hábitos</h2>
      <ul>
        <li v-for="habit in habits" :key="habit.id">
          <habit-item
            :habit="habit"
            @mark-progress="markHabitProgress(habit.id)"
          />
        </li>
      </ul>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import HabitItem from "./components/HabitItem.vue";

const habits = ref([]);
const newHabit = ref("");

const addHabit = () => {
  if (newHabit.value.trim()) {
    habits.value.push({
      id: Date.now(),
      name: newHabit.value,
      progress: [],
    });
    newHabit.value = "";
  }
};

const markHabitProgress = (habitId) => {
  const habit = habits.value.find((h) => h.id === habitId);
  habit.progress.push(new Date().toLocaleDateString());
};
</script>

<style>
#app {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  font-family: Arial, sans-serif;
}

.habits-list {
  margin-top: 20px;
}

input {
  padding: 10px;
  margin-right: 10px;
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
