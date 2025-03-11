<template>
  <div class="rounded-lg bg-slate-800 border border-slate-700 shadow-lg">
    <div id="containerInputs" class="flex items-center p-3">
      <input
        type="text"
        v-model="message"
        placeholder="Write a message..."
        class="flex-grow bg-slate-700 text-white placeholder-slate-400 px-4 py-3 rounded-l-lg focus:outline-none focus:ring-2 focus:ring-blue-500"
        @keyup.enter="handleButton"
      />
      <button 
        class="cursor-pointer bg-blue-600 hover:bg-blue-700 text-white px-4 py-3 rounded-r-lg transition-colors duration-200 flex items-center justify-center"
        @click="handleButton"
        :disabled="!message.trim()"
      >
        <span class="material-symbols-outlined">send</span>
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref, defineEmits } from 'vue';

const emit = defineEmits([ 'send-message' ])

const message = ref("");

const handleButton = async () => {
  if (!message.value.trim()) {
    return false;
  }
  emit('send-message', message.value);
  message.value = "";
};
</script>