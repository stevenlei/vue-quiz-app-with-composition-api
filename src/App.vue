<script setup>
import { ref, reactive, computed } from "vue";

const currentQuestionIndex = ref(0);
const questions = reactive([
  {
    id: 1,
    question: "<h1></h1> 是什麼標籤？",
    answers: [
      { text: "標題", isCorrect: true },
      { text: "段落", isCorrect: false },
      { text: "連結", isCorrect: false },
      { text: "清單", isCorrect: false },
    ],
    selectedIndex: null,
  },
  {
    id: 2,
    question: "<p></p> 是什麼標籤？",
    answers: [
      { text: "標題", isCorrect: false },
      { text: "段落", isCorrect: true },
      { text: "連結", isCorrect: false },
      { text: "清單", isCorrect: false },
    ],
    selectedIndex: null,
  },
  {
    id: 3,
    question: "<a></a> 是什麼標籤？",
    answers: [
      { text: "標題", isCorrect: false },
      { text: "段落", isCorrect: false },
      { text: "連結", isCorrect: true },
      { text: "清單", isCorrect: false },
    ],
    selectedIndex: null,
  },
  {
    id: 4,
    question: "<ul></ul> 是什麼標籤？",
    answers: [
      { text: "標題", isCorrect: false },
      { text: "段落", isCorrect: false },
      { text: "連結", isCorrect: false },
      { text: "清單", isCorrect: true },
    ],
    selectedIndex: null,
  },
]);

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
</script>

<template>
  <div class="min-h-screen p-20 bg-slate-100 flex flex-col items-center">
    <h1 class="text-4xl font-bold">JavaScript Quiz!</h1>

    <div
      class="
        flex
        mt-12
        mb-6
        max-w-3xl
        justify-between
        items-center
        w-full
        text-xl text-slate-700
      "
    >
      <span
        >第 {{ currentQuestionIndex + 1 }} 題，已回答
        {{ answeredQuestions }} 題，合共 {{ questions.length }} 題。</span
      >
      <button
        class="
          bg-blue-700
          text-white
          px-4
          py-2
          rounded
          shadow
          hover:bg-blue-800
        "
      >
        提交
      </button>
    </div>

    <div
      class="
        rounded-xl
        overflow-hidden
        block
        w-full
        max-w-3xl
        shadow-xl
        bg-white
      "
    >
      <h2 class="p-6 bg-blue-800 text-white font-bold text-3xl">
        {{ questions[currentQuestionIndex].question }}
      </h2>
      <ul>
        <li
          v-for="(answer, index) in questions[currentQuestionIndex].answers"
          :key="index"
          class="
            p-6
            bg-slate-50
            border-b-2 border-white
            text-2xl text-slate-700
            hover:bg-slate-300
            cursor-pointer
          "
          :class="{
            'bg-slate-300':
              questions[currentQuestionIndex].selectedIndex === index,
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
            'cursor-not-allowed hover:bg-slate-300 text-slate-300':
              currentQuestionIndex === 0,
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
            'cursor-not-allowed hover:bg-slate-300 text-slate-300':
              currentQuestionIndex === questions.length - 1,
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
  </div>
</template>