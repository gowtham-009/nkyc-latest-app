<template>
    <div>
    <InputText id="email"  class="w-full py-2"  v-model="email" variant="filled" placeholder="Enter Email"size="large"    @blur="validateEmail" />
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
  