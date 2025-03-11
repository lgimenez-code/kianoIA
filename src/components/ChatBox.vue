<template>
  <div id="containerChat" class="flex-grow overflow-auto rounded-lg bg-slate-800 border border-slate-700 shadow-lg mb-4 p-4">
    <div v-if="messages.length === 0" class="flex items-center justify-center h-full">
      <p class="text-slate-500 italic">Send a message to start the conversation...</p>
    </div>    
    <ul v-else class="space-y-4">
      <li v-for="(item, i) in messages" :key="i" class="flex flex-col space-y-2">
        <div class="flex justify-end">
          <div class="bg-blue-600 px-4 py-2 rounded-lg rounded-tr-none max-w-3/4 text-white shadow">
            {{ item.ask }}
          </div>
        </div>            
        <div class="flex justify-start">
          <div 
            class="px-4 py-2 rounded-lg rounded-tl-none max-w-3/4 shadow"
            :class="item.success ? 'bg-slate-700 text-white' : 'bg-red-800 text-white'"
          >
            {{ item.answer }}
          </div>
        </div>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { watch, defineProps, nextTick } from 'vue';

const props = defineProps({
  messages: {
    type: Array,
    required: false,
    default: [],
  }
});

const scrollToBottom = async () => {
  await nextTick();
  const container = document.getElementById("containerChat");
  if (container) {
    container.scrollTop = container.scrollHeight;
  }
};

watch(props.messages, () => {
  if (props.messages.length) {
    scrollToBottom();
  }
});
</script>

<style scoped>
#containerChat::-webkit-scrollbar {
  width: 6px;
}

#containerChat::-webkit-scrollbar-track {
  background: rgba(0, 0, 0, 0.1);
  border-radius: 10px;
}

#containerChat::-webkit-scrollbar-thumb {
  background: rgba(100, 116, 139, 0.5);
  border-radius: 10px;
}

#containerChat::-webkit-scrollbar-thumb:hover {
  background: rgba(100, 116, 139, 0.8);
}
</style>