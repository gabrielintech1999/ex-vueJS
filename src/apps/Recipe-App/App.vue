<template>
  <div id="app">
    <h1>Recipe App</h1>
    <input v-model="searchQuery" placeholder="Buscar receitas..." />
    <button @click="showAddRecipe">Adicionar Nova Receita</button>

    <div v-if="isAddingRecipe">
      <add-recipe @add-recipe="addRecipe" @cancel="isAddingRecipe = false" />
    </div>

    <div v-if="selectedRecipe">
      <recipe-details :recipe="selectedRecipe" @close="selectedRecipe = null" />
    </div>

    <div v-if="!selectedRecipe && !isAddingRecipe">
      <h2>Lista de Receitas</h2>
      <ul>
        <li v-for="recipe in filteredRecipes" :key="recipe.id" @click="selectRecipe(recipe)">
          {{ recipe.name }}
        </li>
      </ul>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";
import AddRecipe from "./components/AddRecipe.vue";
import RecipeDetails from "./components/RecipeDetails.vue";

const recipes = ref([
  { id: 1, name: "Spaghetti", type: "Italiana", ingredients: ["Massa", "Molho de tomate", "Queijo"] },
  { id: 2, name: "Tacos", type: "Mexicana", ingredients: ["Tortilha", "Carne", "Queijo"] },
]);

const searchQuery = ref("");
const selectedRecipe = ref(null);
const isAddingRecipe = ref(false);

const filteredRecipes = computed(() =>
  recipes.value.filter((recipe) =>
    recipe.name.toLowerCase().includes(searchQuery.value.toLowerCase())
  )
);

const selectRecipe = (recipe) => {
  selectedRecipe.value = recipe;
};

const addRecipe = (newRecipe) => {
  newRecipe.id = recipes.value.length + 1;
  recipes.value.push(newRecipe);
  isAddingRecipe.value = false;
};

const showAddRecipe = () => {
  isAddingRecipe.value = true;
};
</script>

<style>
#app {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  font-family: Arial, sans-serif;
}

ul {
  list-style: none;
  padding: 0;
}

li {
  padding: 10px;
  border-bottom: 1px solid #ddd;
  cursor: pointer;
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
