


<!-- <script setup>
  import { ref } from "vue";

  const newValue = ref("")

  console.log(newValue.value);
  

  async function getData() {

    const apiKey = "be7333a154937ee1b9131c3cf5221405"
    const res = await fetch(`https://api.openweathermap.org/data/2.5/weather?q=${"Angola"}&appid=${apiKey}`)

    const data = await res.json()

    console.log(data);
    
  }

  getData()

</script>

<template>
  <input type="text" v-model="newValue">
  <h1 v-if="newValue">{{ newValue }}</h1>
  <h1>Hello App weather</h1>
</template> -->

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
