<template>
  <header class="text-center mb-4">
    <h1 class="text-2xl font-bold text-white">{{ title }}</h1>
  </header>
</template>

<script setup>
import { defineProps } from 'vue'; 

defineProps({
  title: String,
})
</script>