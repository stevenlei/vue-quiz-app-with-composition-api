<script setup>
import { ref, reactive, computed, onMounted } from "vue";

const currentQuestionIndex = ref(0);
const isSubmitted = ref(false);
const questions = reactive([]);

const prevQuestion = () => {
  if (currentQuestionIndex.value > 0) {
    currentQuestionIndex.value--;
  }
};

const nextQuestion = () => {
  if (currentQuestionIndex.value < questions.length - 1) {
    currentQuestionIndex.value++;
  }
};

const answeredQuestions = computed(() => {
  return questions.filter((one) => one.selectedIndex !== null).length;
});

const selectAnswer = (questionIndex, answerIndex) => {
  if (questions[questionIndex].selectedIndex == answerIndex) {
    // de-select
    questions[questionIndex].selectedIndex = null;
  } else {
    questions[questionIndex].selectedIndex = answerIndex;
  }
};

const submit = () => {
  isSubmitted.value = true;
};

const score = computed(() => {
  return Math.floor(
    (questions.filter((one) => {
      return one.answers[one.selectedIndex] && one.answers[one.selectedIndex].isCorrect;
    }).length /
      questions.length) *
      100,
    1
  );
});

onMounted(async () => {
  const response = await fetch("https://codingstartup.com/quiz/data.php");
  const data = await response.json();
  questions.push(...data);
});
</script>

<template>
  <div class="min-h-screen p-20 bg-slate-100 flex flex-col items-center">
    <h1 class="text-6xl font-bold">HTML Basic Quiz</h1>
    <template v-if="questions.length > 0">
      <template v-if="isSubmitted">
        <div class="bg-slate-300 px-16 py-8 mt-12 rounded-2xl mb-12">
          <h4 class="text-xl text-center">總分</h4>
          <h2 class="text-center text-6xl font-bold mt-4">{{ score }}</h2>
        </div>
        <div
          v-for="question in questions"
          :key="question.id"
          class="rounded-xl overflow-hidden block w-full max-w-3xl shadow-xl bg-white mb-12"
        >
          <h2 class="p-6 bg-blue-800 text-white font-bold text-3xl">
            {{ question.question }}
          </h2>
          <ul>
            <li
              v-for="(answer, index) in question.answers"
              :key="index"
              class="p-6 bg-slate-50 border-b-2 border-white text-2xl text-slate-700 cursor-pointer"
              :class="{
                'bg-green-300': answer.isCorrect,
                'bg-red-300': question.selectedIndex === index && !answer.isCorrect,
              }"
            >
              {{ answer.text }}
            </li>
          </ul>
        </div>
      </template>

      <template v-if="!isSubmitted">
        <div class="flex mt-12 mb-6 max-w-3xl justify-between items-center w-full text-xl text-slate-700">
          <span
            >第 {{ currentQuestionIndex + 1 }} 題，已回答 {{ answeredQuestions }} 題，合共
            {{ questions.length }} 題。</span
          >
          <button
            class="bg-blue-700 text-white px-4 py-2 rounded shadow hover:bg-blue-800 disabled:bg-blue-300"
            @click="submit"
            :disabled="answeredQuestions < questions.length"
          >
            提交
          </button>
        </div>

        <div class="rounded-xl overflow-hidden block w-full max-w-3xl shadow-xl bg-white">
          <h2 class="p-6 bg-blue-800 text-white font-bold text-3xl">
            {{ questions[currentQuestionIndex].question }}
          </h2>
          <ul>
            <li
              v-for="(answer, index) in questions[currentQuestionIndex].answers"
              :key="index"
              class="p-6 border-b-2 border-white text-2xl text-slate-700 hover:bg-slate-300 cursor-pointer"
              :class="{
                'bg-slate-300': questions[currentQuestionIndex].selectedIndex === index,
                'bg-slate-50': questions[currentQuestionIndex].selectedIndex !== index,
              }"
              @click="selectAnswer(currentQuestionIndex, index)"
            >
              {{ answer.text }}
            </li>
          </ul>
        </div>

        <div class="flex mt-12 mb-6">
          <ul class="flex bg-slate-300 rounded-xl overflow-hidden">
            <li
              class="px-4 py-3 cursor-pointer"
              :class="{
                'cursor-not-allowed hover:bg-slate-300 text-slate-300': currentQuestionIndex === 0,
                'hover:bg-slate-400': currentQuestionIndex !== 0,
              }"
              @click="prevQuestion"
            >
              <svg
                xmlns="http://www.w3.org/2000/svg"
                class="inline-block w-4 h-4"
                :class="{ 'fill-slate-400': currentQuestionIndex === 0 }"
                viewBox="0 0 24 24"
              >
                <path
                  d="M4.5,12a2.3,2.3,0,0,1,.78-1.729L16.432.46a1.847,1.847,0,0,1,2.439,2.773L9.119,11.812a.25.25,0,0,0,0,.376l9.752,8.579a1.847,1.847,0,1,1-2.439,2.773L5.284,13.732A2.31,2.31,0,0,1,4.5,12Z"
                ></path>
              </svg>
            </li>
            <li
              class="px-4 py-3 cursor-pointer"
              :class="{
                'cursor-not-allowed hover:bg-slate-300 text-slate-300': currentQuestionIndex === questions.length - 1,
                'hover:bg-slate-400': currentQuestionIndex !== questions.length - 1,
              }"
              @click="nextQuestion"
            >
              <svg
                xmlns="http://www.w3.org/2000/svg"
                class="inline-block w-4 h-4"
                :class="{
                  'fill-slate-400': currentQuestionIndex === questions.length - 1,
                }"
                viewBox="0 0 24 24"
              >
                <path
                  d="M19.5,12a2.3,2.3,0,0,1-.78,1.729L7.568,23.54a1.847,1.847,0,0,1-2.439-2.773l9.752-8.579a.25.25,0,0,0,0-.376L5.129,3.233A1.847,1.847,0,0,1,7.568.46l11.148,9.808A2.31,2.31,0,0,1,19.5,12Z"
                ></path>
              </svg>
            </li>
          </ul>
        </div>
      </template>
    </template>
    <template v-else>
      <svg
        class="animate-spin w-8 h-8 text-gray-500 mt-20"
        xmlns="http://www.w3.org/2000/svg"
        fill="none"
        viewBox="0 0 24 24"
      >
        <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
        <path
          class="opacity-75"
          fill="currentColor"
          d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"
        ></path>
      </svg>
    </template>
  </div>
</template>
