<template>
    <div class="container">
     <h1>tenzie game is the next...</h1>
     <ul>
       <li v-for="die in dice" :key="die.id" >
         <button :class="{ selected: die.isSelected  }" class="die" @click="selectDice(die.id)">
           {{ die.value }}
         </button>
       </li>
     </ul>
     <button @click="rollDice">roll dice</button>
    </div>
   </template>
   
   <script setup>
   import { computed, ref } from "vue";
   
   const generateDice = () => {
     console.log("ok");
   
     return Array.from({ length: 10 }, (_, i) => ({
       id: i + 1,
       value: Math.ceil(Math.random() * 6),
       isSelected: false,
     }));
   };
   
   const dice = ref(generateDice());
   
   const rollDice = () => {
     console.log("OK");
   
     dice.value = dice.value.map((die) =>
       die.isSelected ? die : { ...die, value: Math.ceil(Math.random() * 6) }
     );
   };
   
   const selectDice = (idSelected) => {
     dice.value = dice.value.map((die) =>
       die.id !== idSelected ? die : { ...die, isSelected: !die.isSelected }
     );
   };
   
   /*
   const generateDice = () => {
   
     console.log("OK");
     
     
     for (let i = 0; i < 10; i++) {
       
       dice.value.push({
         id: Date.now(),
         value: Math.ceil(Math.random() * 6),
         isSelected: true
       })
       
     }
   
   }*/
   </script>
   
   <style scoped>
   ul {
     display: grid;
     grid-template-columns: repeat(5, minmax(30px, 50px));
     gap: 10px;
     text-align: center;
   
     margin: 25px auto;
     max-width: 360px;
     justify-content: center;
     /* border: 1px solid red; */
   }
    li {
     list-style: none;
   }
   
   .die {
     width: 50px;
     height: 50px;
     background-color: #fff;
     color: #fff;
     border-radius: 4px;
     cursor: pointer;
     text-align: center;
     padding: 15px;
     margin: 0 auto;
     display: block;
     border: none;
     color: #000;
     font-weight: bold;
     font-size: 1.1rem;
   }
   
   .selected {
     background-color: blue;
   }
   </style>