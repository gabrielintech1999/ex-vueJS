<template>
    <div class="habit-item">
      <h3>{{ habit.name }}</h3>
      <button @click="markProgress">Marcar Progresso</button>
      <div v-if="habit.progress.length > 0">
        <h4>Progresso:</h4>
        <ul>
          <li v-for="(date, index) in habit.progress" :key="index">{{ date }}</li>
        </ul>
      </div>
    </div>
  </template>
  
  <script setup>
  const props = defineProps({
    habit: Object,
  });
  
  const emit = defineEmits(["mark-progress"]);
  
  const markProgress = () => {
    emit("mark-progress");
  };
  </script>
  
  <style>
  .habit-item {
    border: 1px solid #ddd;
    padding: 10px;
    margin: 10px 0;
  }
  </style>
  