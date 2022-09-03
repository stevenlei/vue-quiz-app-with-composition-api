<script setup>
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
      <span>第 1 題，已回答 1 題，合共 10 題。</span>
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
        JavaScript 與 Java 有什麼關係？
      </h2>
      <ul>
        <li
          class="
            p-6
            bg-slate-50
            border-b-2 border-white
            text-2xl text-slate-700
            hover:bg-slate-300
            cursor-pointer
          "
        >
          JavaScript 是 Java 的一個 Library
        </li>
        <li
          class="
            p-6
            bg-slate-50
            border-b-2 border-white
            text-2xl text-slate-700
            hover:bg-slate-300
            cursor-pointer
          "
        >
          JavaScript 使用 Java 語言
        </li>
        <li
          class="
            p-6
            bg-slate-50
            border-b-2 border-white
            text-2xl text-slate-700
            hover:bg-slate-300
            cursor-pointer
          "
        >
          JavaScript 與 Java 沒有關係
        </li>
        <li
          class="
            p-6
            bg-slate-50
            border-b-2 border-white
            text-2xl text-slate-700
            hover:bg-slate-300
            cursor-pointer
          "
        >
          JavaScript 與 Java 由相同的公司所開發
        </li>
      </ul>
    </div>

    <div class="flex mt-12 mb-6">
      <ul class="flex bg-slate-300 rounded-xl overflow-hidden">
        <li class="hover:bg-slate-400 px-4 py-3 cursor-pointer">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            class="inline-block w-4 h-4"
            viewBox="0 0 24 24"
          >
            <path
              d="M4.5,12a2.3,2.3,0,0,1,.78-1.729L16.432.46a1.847,1.847,0,0,1,2.439,2.773L9.119,11.812a.25.25,0,0,0,0,.376l9.752,8.579a1.847,1.847,0,1,1-2.439,2.773L5.284,13.732A2.31,2.31,0,0,1,4.5,12Z"
            ></path>
          </svg>
        </li>
        <li class="hover:bg-slate-400 px-4 py-3 cursor-pointer">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            class="inline-block w-4 h-4"
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