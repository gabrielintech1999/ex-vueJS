<template>
  <div class="weather-app">
    <h1>Weather App</h1>

    <input
      type="text"
      v-model="city"
      placeholder="Enter city name"
      @keyup.enter="getWeather"
    />

    <button @click="getWeather">Get Weather</button>

    <div v-if="weather">
      <h2>{{ weather.name }}</h2>
      <p>{{ weather.weather[0].description }}</p>
      <p>Temperature: {{ (weather.main.temp - 273.15).toFixed(2) }}°C</p>
      <p>Humidity: {{ weather.main.humidity }}%</p>
      <p>Wind Speed: {{ weather.wind.speed }} m/s</p>
    </div>

    <div v-if="errorMessage" class="error">{{ errorMessage }}</div>
  </div>
</template>

<script setup>
import { ref } from "vue";
// Estado reativo para a cidade e o clima
const city = ref("");
const weather = ref(null);
const errorMessage = ref("");

// Função para buscar o clima usando a API
const getWeather = async () => {
  const apiKey = "be7333a154937ee1b9131c3cf5221405";

  try {
    const res = await fetch(
      `https://api.openweathermap.org/data/2.5/weather?q=${city.value}&appid=${apiKey}`
    );

    const data = await res.json();

    console.log(data);

    weather.value = data;
    errorMessage.value = "";
  } catch (error) {
    errorMessage.value = "City not found. Please try again.";
    weather.value = null;
  }
};
</script>

<style scoped>
.weather-app {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
  font-family: "Arial", sans-serif;
  background-color: #f0f0f0;
  padding: 20px;
}

h1 {
  font-size: 2rem;
  margin-bottom: 20px;
}

input {
  padding: 10px;
  font-size: 1rem;
  margin-bottom: 10px;
  border-radius: 5px;
  border: 1px solid #ccc;
}

button {
  padding: 10px 20px;
  font-size: 1rem;
  cursor: pointer;
  background-color: #4caf50;
  color: white;
  border: none;
  border-radius: 5px;
  transition: background-color 0.3s ease;
}

button:hover {
  background-color: #45a049;
}

h2 {
  font-size: 1.5rem;
  margin-top: 20px;
}

.error {
  color: red;
  margin-top: 20px;
}
</style>
