<template>
    <div>

      <FloatLabel variant="in">
    <InputText id="email"  class="w-full"  v-model="email" variant="filled"      @blur="validateEmail" />
    <label for="in_label">Email ID*</label>
</FloatLabel>


   
     
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';


  
  const props = defineProps(['modelValue']);
  const emit = defineEmits(['update:modelValue']);
  
  const email = ref(props.modelValue || '');

  const validateEmail = () => {
    const emailPattern = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    if (!emailPattern.test(email.value)) {
      console.log('Please enter a valid email address')
    } else {
      
    }
  };

  watch(email, (newValue) => {
    emit('update:modelValue', newValue);
  });
  </script>
  
  <style>
  .text-red-500 {
    color: #ef4444; /* Tailwind error color */
  }
  </style>
  