<script setup>
import { ref, computed } from "vue";

const questions = ref([
  {
    question: "Which of the following lets you create a variable?",
    answer: 3,
    options: ["let", "const", "var", "all of the above"],
    selected: null,
  },

  {
    question:
      "Which method removes the last element from an array and returns that element?",
    answer: 2,
    options: ["last()", "get()", "pop()"],
    selected: null,
  },

  {
    question:
      "Which method returns the calling string value converted to upper case?",
    answer: 0,
    options: ["toUppperCase()", "toCapital()", "toLocaleStringUpperCase()"],
    selected: null,
  },
]);
</script>

<template>
  <h1 class="text-blue-500">hello world</h1>
</template>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Montserrat", sans-serif;
}
body {
  background-color: #ffffff;
}
</style>
