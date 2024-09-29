<script setup>
import { ref } from "vue";

const count = ref(0);

const increment = () => {
  count.value = count.value + 1;

  console.log(count.value);
};

const decrement = () => {
  count.value = count.value - 1;

  console.log(count.value);
};

const reset = () => {
  count.value = 0;

  console.log(count.value);
};
</script>

<template>
  <div class="counter">
    <div>{{ count }}</div>
    <button @click="increment">Increment</button>
    <button @click="reset">Reset</button>
    <button @click="decrement">Decrement</button>
  </div>
</template>

<style scoped>
.counter {
  border: 2px solid red;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  gap: 5px;
}
</style>