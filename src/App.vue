<template>
    <h1>Expense Tracker</h1>
    <form  @submit.prevent="addExpense" >
      <input v-model="description" placeholder="Description..." type="text" name="" id="">
      <input v-model="amount" placeholder="Amount..." type="number" name="" id="">

      <select  v-model="category" name="" id="">
        <option>Transport</option>
        <option>Food</option>
        <option>Internet</option>
      </select>

      <button type="submit">Add Expense</button>
    </form>
    <div class="expense">
        <h1>Expenses</h1>

        <u>
          <li v-for="expense in expenses"  >
            <span>{{ expense.description  }}  {{ expense.amount }}KZ ({{expense.category}})</span>
          </li>
        </u>
    </div>
</template>

<script setup >
import { ref } from 'vue';



const amount = ref("")
const description = ref("")
const category = ref("Food")
const expenses = ref([])

let n = new Date().toISOString()
console.log(n.slice(0, 10));



    const addExpense = () => {
        
      expenses.value.push({
        id: Date.now(),
        description: description.value,
        amount: parseFloat(amount.value),
        category: category.value,
        date: new Date().toISOString().slice(0, 10)

      })


        
    }
</script>

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
