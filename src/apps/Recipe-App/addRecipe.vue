<template>
    <div class="add-recipe">
      <h2>Adicionar Nova Receita</h2>
      <label for="name">Nome da Receita:</label>
      <input v-model="name" id="name" />
  
      <label for="type">Tipo de Cozinha:</label>
      <input v-model="type" id="type" />
  
      <label for="ingredients">Ingredientes (separados por vírgula):</label>
      <input v-model="ingredients" id="ingredients" />
  
      <button @click="submitRecipe">Adicionar</button>
      <button @click="$emit('cancel')">Cancelar</button>
    </div>
  </template>
  
  <script setup>
  import { ref } from "vue";
  
  const name = ref("");
  const type = ref("");
  const ingredients = ref("");
  
  const submitRecipe = () => {
    const newRecipe = {
      name: name.value,
      type: type.value,
      ingredients: ingredients.value.split(","),
    };
    $emit("add-recipe", newRecipe);
  };
  </script>
  
  <style>
  .add-recipe {
    border: 1px solid #ddd;
    padding: 20px;
    margin: 20px 0;
  }
  </style>
  