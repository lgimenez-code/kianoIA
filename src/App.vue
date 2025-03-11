<template>
  <main class="flex min-h-screen flex-col bg-slate-900">
    <div class="container m-auto">
      <div if="containerChat" class="container-border h-200">
        <ul v-for="(item, i) in arrayMessages" :key="i">
          <li class="my-2 text-right">{{ item.ask }}</li>
          <li
            class="my-2 text-left"
            :class="{ 'text-red-600': !item.success }"
          >{{ item.answer }}</li>
        </ul>
      </div>
      <div class="mt-4 container-border rounded-lg">
        <div id="containerInputs" class="flex flex-row my-2 mx-2 h-12">
          <input
            type="text"
            v-model="message"
            class="container-border w-full text-gray-500 text-lg"
          />
          <button class="flex ml-2" @click="handleButton">
            <span class="material-symbols-outlined cursor-pointer m-auto text-[40px]!">
              send
            </span>
          </button>
        </div>
      </div>
    </div>
  </main>
</template>

<script setup>
import { ref } from "vue";
import { SendMessage } from "./api/gemini.js";

const message = ref("");
const arrayMessages = ref([]);

const handleButton = async () => {
  try {
    const answer = await SendMessage(message.value);
    arrayMessages.value.push({
      ask: message.value,
      answer: answer,
      success: true,
    });
  } catch (error) {
    arrayMessages.value.push({
      ask: message.value,
      answer: `An error has ocurred, ${error}`,
      success: false,
    });
  }
};
</script>

<style scoped></style>
