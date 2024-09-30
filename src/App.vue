<template>
  <header>
    <h3>Meme Generator</h3>
  </header>
  <div class="container">
    <form>
      <input v-model="meme.top" type="text" placeholder="Top..." />
      <input v-model="meme.bottom" type="text" placeholder="bottom..." />
      <button @click="getRandomMemeImg" type="button">
        Get a new meme image
      </button>
    </form>

    <div class="wrapper">
      <span class="top">{{ meme.top }}</span>
      <img v-if="!isloading" :src="meme.imgCover" alt="meme image" />
      <div class="spinner" v-else></div>
      <span class="bottom">{{ meme.bottom }}</span>
    </div>
  </div>
</template>

<script setup>
import { onMounted, ref } from "vue";

const isloading = ref(true);

let memes = [];

const meme = ref({
  top: "",
  bottom: "",
  imgCover: "",
});

const getMemes = async () => {
  try {
    const res = await fetch("https://api.imgflip.com/get_memes");
    const data = await res.json();

    memes = data.data.memes;

    isloading.value = !isloading.value;
    getRandomMemeImg()
    //console.log(data.data.memes);
  } catch (error) {
    console.log("Error");
  }
};

const getRandomMemeImg = () => {
  const randomIndex = Math.floor(Math.random() * memes.length);

  const { url } = memes[randomIndex];

  meme.value.imgCover = url;

  console.log(url);
};

onMounted(() => {
  getMemes();
});
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
