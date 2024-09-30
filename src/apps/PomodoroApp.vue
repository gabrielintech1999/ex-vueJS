<template>
    <div class="pomodoro"  >
      <h1>Pomodoro Timer</h1>
      <div class="timer">
        <h2>{{ formatTime(remainingTime) }}</h2>
      </div>
      <div class="controls">
        <button @click="startTimer" v-if="!isRunning">Iniciar</button>
        <button @click="pauseTimer" v-if="isRunning">Pausar</button>
        <button @click="resetTimer">Resetar</button>
      </div>
      <div class="status">
        <p>Status: {{ isBreak ? 'Pausa' : 'Trabalho' }}</p>
      </div>
    </div>
  </template>
  
  <script>
  import { ref, onUnmounted } from "vue";
  
  export default {
    setup() {
      const workTime = 25 * 60; // 25 minutos em segundos
      const breakTime = 5 * 60; // 5 minutos em segundos
      const remainingTime = ref(workTime);
      const isRunning = ref(false);
      const isBreak = ref(false);
      let interval;
  
      const startTimer = () => {
        isRunning.value = true;
        interval = setInterval(() => {
          if (remainingTime.value > 0) {
            remainingTime.value--;
          } else {
            toggleSession();
          }
        }, 1000);
      };
  
      const pauseTimer = () => {
        isRunning.value = false;
        clearInterval(interval);
      };
  
      const resetTimer = () => {
        clearInterval(interval);
        isRunning.value = false;
        remainingTime.value = isBreak.value ? breakTime : workTime;
      };
  
      const toggleSession = () => {
        isBreak.value = !isBreak.value;
        remainingTime.value = isBreak.value ? breakTime : workTime;
      };
  
      const formatTime = (timeInSeconds) => {
        const minutes = Math.floor(timeInSeconds / 60); // converte segundos em minutos
        const seconds = timeInSeconds % 60; // da o resto dos segundos que falta
        return `${minutes.toString().padStart(2, '0')}:${seconds
          .toString()
          .padStart(2, '0')}`;
      };
  
      // Limpar o intervalo ao desmontar o componente
      onUnmounted(() => {
        clearInterval(interval);
      });
  
      return {
        remainingTime,
        isRunning,
        isBreak,
        startTimer,
        pauseTimer,
        resetTimer,
        formatTime,
      };
    },
  };
  </script>
  
  <style>
  .pomodoro {
    max-width: 400px;
    margin: 50px auto;
    text-align: center;
  }
  
  .timer {
    font-size: 48px;
    margin-bottom: 20px;
  }
  
  .controls button {
    margin: 10px;
    padding: 10px 20px;
    font-size: 16px;
  }
  
  .status {
    font-size: 18px;
    margin-top: 20px;
  }
  </style>
  