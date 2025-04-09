<template>
    <div class="w-full">
      <span class="text-lg text-gray-500">Nominee's name</span>
      <InputText
        type="text"
        v-model="name"
        variant="filled"
        class="w-full py-2"
        @keypress="allowAlphaOnly"
        @input="formatName"
         size="large"
        placeholder="Enter nominee's name"
      />
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  
  const name = ref('');
  
  // Allow only A-Z, space, and dot (.)
  const allowAlphaOnly = (event) => {
    const char = event.key.toUpperCase();
    const regex = /^[A-Z.\s]$/;
    if (!regex.test(char)) {
      event.preventDefault();
    }
  };
  
  // Auto format input to uppercase and remove disallowed characters
  const formatName = () => {
    name.value = name.value.toUpperCase().replace(/[^A-Z.\s]/g, '');
  };
  </script>
  