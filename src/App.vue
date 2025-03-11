<template>
  <main class="main">
    <div class="containerApp">
      <Header :title="'Chat IA'"/>
      <ChatBox :messages="arrayMessages" />
      <UserInput @send-message="handleMessage" />
    </div>
  </main>
</template>

<script setup>
import { ref } from "vue";
import Header from "./components/Header.vue";
import ChatBox from "./components/ChatBox.vue";
import UserInput from "./components/UserInput.vue";
import { SendMessage } from "./api/service.js";

const arrayMessages = ref([]);
const isLoading = ref(false);

const handleMessage = async (userMessage) => {
  // type a "Writing..." message
  arrayMessages.value.push({
    ask: userMessage,
    answer: "Writing...",
    success: true,
  });
  
  try {
    isLoading.value = true;
    const answer = await SendMessage(userMessage);
    
    const lastIndex = arrayMessages.value.length - 1;
    // update the "Writing..." message with the actual response
    arrayMessages.value[lastIndex] = {
      ask: userMessage,
      answer: answer,
      success: true,
    };
  } catch (error) {
    const lastIndex = arrayMessages.value.length - 1;
    // update the "Writing..." message with the error
    arrayMessages.value[lastIndex] = {
      ask: userMessage,
      answer: `An error has ocurred : ${error.message || error}`,
      success: false,
    };
  } finally {
    isLoading.value = false;
  }
}



</script>