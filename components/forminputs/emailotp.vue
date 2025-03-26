<template>
    <div>
      <div class="card flex justify-center">
        <InputOtp 
          v-model="emailotp" 
          :length="6" 
          size="large" 
          @input="validateOtp"
        />
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref, watch } from 'vue';
  const props = defineProps(['modelValue']);
  const emit = defineEmits(['update:modelValue']);

  const emailotp = ref(props.modelValue || '');
  
  function validateOtp() {
    emailotp.value = emailotp.value.replace(/\D/g, ''); // Remove non-numeric characters
  }

  watch(emailotp, (newValue) => {
    emit('update:modelValue', newValue);
  });
  </script>
  
  <style scoped>
  </style>
  