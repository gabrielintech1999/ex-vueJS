<template>
    <div>
      <h1>Currency Converter</h1>
      <div>
        <label>Amount:</label>
        <input v-model="amount" type="number" placeholder="Enter amount" />
      </div>
      <div>
        <label>From:</label>
        <select v-model="fromCurrency">
          <option v-for="currency in currencies" :key="currency" :value="currency">{{ currency }}</option>
        </select>
      </div>
      <div>
        <label>To:</label>
        <select v-model="toCurrency">
          <option v-for="currency in currencies" :key="currency" :value="currency">{{ currency }}</option>
        </select>
      </div>
      <button @click="convertCurrency">Convert</button>
      <p v-if="convertedAmount">Converted Amount: {{ convertedAmount }} {{ toCurrency }}</p>
    </div>
  </template>
  
  <script setup>
  import { ref, onMounted } from 'vue';
  
  const amount = ref(1);
  const fromCurrency = ref('USD');
  const toCurrency = ref('EUR');
  const convertedAmount = ref(null);
  const currencies = ref([]);
  const apiKey = 'YOUR_API_KEY'; // Substitua pela sua chave de API
  
  const fetchCurrencies = async () => {
    const response = await fetch(`https://api.exchangerate-api.com/v4/latest/USD`);
    const data = await response.json();
    currencies.value = Object.keys(data.rates);
  };
  
  const convertCurrency = async () => {
    const response = await fetch(
      `https://api.exchangerate-api.com/v4/latest/${fromCurrency.value}`
    );
    const data = await response.json();
    const rate = data.rates[toCurrency.value];
    convertedAmount.value = (amount.value * rate).toFixed(2);
  };
  
  onMounted(() => {
    fetchCurrencies();
  });
  </script>
  
  <style scoped>
  h1 {
    color: #333;
  }
  
  input,
  select {
    margin: 5px 0;
  }
  </style>
  