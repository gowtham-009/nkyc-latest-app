<template>
    <div class="w-full">
      <span class="text-lg text-gray-500">State</span>
      <InputText
        type="text"
        v-model="state"
        variant="filled"
        class="w-full py-2"
        @keypress="allowAlphaOnly"
        @input="formatstate"
         size="large"
        placeholder="Enter state"
      />
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  
  const state = ref('');
  
  // Allow only A-Z, space, and dot (.)
  const allowAlphaOnly = (event) => {
    const char = event.key.toUpperCase();
    const regex = /^[A-Z.\s]$/;
    if (!regex.test(char)) {
      event.preventDefault();
    }
  };
  
  // Auto format input to uppercase and remove disallowed characters
  const formatstate = () => {
    state.value = state.value.toUpperCase().replace(/[^A-Z.\s]/g, '');
  };
  </script>
  