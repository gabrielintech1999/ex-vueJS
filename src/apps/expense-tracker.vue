<template>
    <div>
      <h1>Expense Tracker</h1>
      <form @submit.prevent="addExpense">
        <input v-model="description" placeholder="Description" required />
        <input v-model="amount" type="number" placeholder="Amount" required />
        <select v-model="category">
          <option>Food</option>
          <option>Transport</option>
          <option>Entertainment</option>
        </select>
        <button type="submit">Add Expense</button>
      </form>
      
      <div v-if="expenses.length">
        <h2>Expenses</h2>
        <ul>
          <li v-for="expense in expenses" :key="expense.id">
            {{ expense.description }} - ${{ expense.amount }} ({{ expense.category }})
          </li>
        </ul>
      </div>
    </div>
  </template>
  
  <script>
  import { ref } from 'vue';
  
  export default {
  
  //   const expenses = ref([
  //   { id: 1, description: 'Groceries', amount: 50, category: 'Food', date: '2024-09-25' },
  //   { id: 2, description: 'Bus ticket', amount: 2.5, category: 'Transport', date: '2024-09-26' },
  // ]);
  
    setup() {
      const description = ref('');
      const amount = ref(0);
      const category = ref('Food');
      const expenses = ref([]);
  
      const addExpense = () => {
        expenses.value.push({
          id: Date.now(),
          description: description.value,
          amount: parseFloat(amount.value),
          category: category.value,
          date: new Date().toISOString().slice(0, 10),
        });
        description.value = '';
        amount.value = 0;
      };
  
      return {
        description,
        amount,
        category,
        expenses,
        addExpense,
      };
    },
  };
  </script>
  