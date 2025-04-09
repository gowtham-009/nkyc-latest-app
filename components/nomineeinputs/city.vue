<template>
    <div class="w-full">
      <span class="text-lg text-gray-500">City</span>
      <InputText
        type="text"
        v-model="city"
        variant="filled"
        class="w-full py-2"
        @keypress="allowAlphaOnly"
        @input="formatcity"
         size="large"
        placeholder="Enter city"
      />
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  
  const city = ref('');
  
  // Allow only A-Z, space, and dot (.)
  const allowAlphaOnly = (event) => {
    const char = event.key.toUpperCase();
    const regex = /^[A-Z.\s]$/;
    if (!regex.test(char)) {
      event.preventDefault();
    }
  };
  
  // Auto format input to uppercase and remove disallowed characters
  const formatcity = () => {
    city.value = city.value.toUpperCase().replace(/[^A-Z.\s]/g, '');
  };
  </script>
  