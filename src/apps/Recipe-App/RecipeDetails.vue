<template>
    <div class="recipe-details">
      <h2>{{ recipe.name }}</h2>
      <p><strong>Tipo:</strong> {{ recipe.type }}</p>
      <h3>Ingredientes:</h3>
      <ul>
        <li v-for="ingredient in recipe.ingredients" :key="ingredient">{{ ingredient }}</li>
      </ul>
      <button @click="$emit('close')">Fechar</button>
    </div>
  </template>
  
  <script setup>
  const props = defineProps({
    recipe: Object,
  });
  </script>
  
  <style>
  .recipe-details {
    border: 1px solid #ddd;
    padding: 20px;
    margin: 20px 0;
  }
  </style>
  