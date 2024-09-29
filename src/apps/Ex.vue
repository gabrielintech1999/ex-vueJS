<script>
export default {
  data() {
    return {
      msg: "Hello Vue!",
      name: "Gabriel",
      numbers: [1, 2, 3, 4]
    };
  },
  methods: {
    clickMe() {
      console.log("OK");
    },
  },
};
</script>

<template>
  <div>Hello {{ numbers.map(num => num) }}</div>
  <button @click="clickMe">Click Me</button>
</template>
