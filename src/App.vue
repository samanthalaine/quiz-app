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

const quizCompleted = ref(false)
const currentQuestion = ref(0)

const score = computed(()=>{
  let value = 0
  questions.value.map(quest => {
    if (quest.selected === quest.answer){
      value++
    }
  })
  return value
})

const getCurrentQuestion = computed(()=>{
  let question = questions.value[currentQuestion.value]
  question.index = currentQuestion.value
  return question
})

const setAnswer = e =>{
  questions.value[currentQuestion.value].selected = e.target.value
  e.target.value = null
}

const nextQuestion = () => {
	if (currentQuestion.value < questions.value.length - 1) {
		currentQuestion.value++
		return
	}
	
	quizCompleted.value = true
}

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
