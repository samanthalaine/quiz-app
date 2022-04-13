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

const quizCompleted = ref(false);
const currentQuestion = ref(0);

const score = computed(() => {
  let value = 0;
  questions.value.map((quest) => {
    if (quest.selected === quest.answer) {
      value++;
    }
  });
  return value;
});

const getCurrentQuestion = computed(() => {
  let question = questions.value[currentQuestion.value];
  question.index = currentQuestion.value;
  return question;
});

const setAnswer = (e) => {
  questions.value[currentQuestion.value].selected = e.target.value;
  e.target.value = null;
};

const nextQuestion = () => {
  if (currentQuestion.value < questions.value.length - 1) {
    currentQuestion.value++;
    return;
  }

  quizCompleted.value = true;
};
</script>

<template>
  <main class="flex justify-center">
    <h1 class="text-3xl font-semibold text-blue-500">JavaScript Quiz</h1>
    <section v-if="!quizCompleted">
      <div>
        <span>{{ getCurrentQuestion.question }}</span>
        <span>Score{{ score }}/{{ questions.length }}</span>
        <div class="form-check">
          <label
            v-for="(option, index) in getCurrentQuestion.options"
            :for="'option' + index"
            :key="index"
            class="inline-block text-gray-800 form-check-label"
            :class="`option ${
              getCurrentQuestion.selected == index
                ? index == getCurrentQuestion.answer
                  ? 'correct'
                  : 'wrong'
                : ''
            } ${
              getCurrentQuestion.selected != null &&
              index != getCurrentQuestion.selected
                ? 'disabled'
                : ''
            }`"
          >
            <input
            class="form-radio"
              type="radio"
              :id="'option' + index"
              :name="getCurrentQuestion.index"
              :value="index"
              v-model="getCurrentQuestion.selected"
              :disabled="getCurrentQuestion.selected"
              @change="setAnswer"
            />
            <span>{{ option }}</span>
          </label>
        </div>
      </div>
      <button 
        class="px-4 py-2 font-bold text-white bg-blue-500 rounded shadow hover:bg-blue-400 focus:shadow-outline focus:outline-none"
				@click="nextQuestion" 
				:disabled="!getCurrentQuestion.selected">
				{{ 
					getCurrentQuestion.index == questions.length - 1 
						? 'Finish' 
						: getCurrentQuestion.selected == null
							? 'Select an option'
							: 'Next question'
				}}
			</button>
    </section>
    <section v-else>
			<h2>You have finished the quiz!</h2>
			<p>Your score is {{ score }}/{{ questions.length }}</p>
		</section>
  </main>
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
