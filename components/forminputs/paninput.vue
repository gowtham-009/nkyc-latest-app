<template>
    <div class="w-full">
      <FloatLabel variant="in">
        <InputText
          id="pan_label"
          class="w-full"
          v-model="pan"
          variant="filled"
          @input="formatInput"
          @keypress="allowAlphanumeric"
          maxlength="10"
        />
        <label for="pan_label">PAN no*</label>
      </FloatLabel>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  
  const pan = ref('');
  
  
  const allowAlphanumeric = (event) => {
    const char = event.key.toUpperCase(); 
    const regex = /^[A-Z0-9]$/; 
  
    if (!regex.test(char)) {
      event.preventDefault();
    }
  };
  
 
  const formatInput = () => {
    pan.value = pan.value.toUpperCase().replace(/[^A-Z0-9]/g, '').slice(0, 10);
  };
  </script>
  