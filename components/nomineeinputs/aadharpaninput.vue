<template>
    <div class="w-full">
      <label for="pan_label" class="text-gray-500 text-lg font-normal">Nominee's PAN or Aadhaar</label>
      <InputText
        id="pan_label"
        class="w-full py-2"
        v-model="panaadhar"
        variant="filled"
        @input="formatInput"
        @keypress="allowAlphanumeric"
        maxlength="10"
        size="large"
        placeholder="Enter pan or aadhaar no"
      />
    </div>
  </template>
  
  <script setup>
  import { ref, watch } from 'vue';
  
  // Props and Emits for v-model compatibility
  const props = defineProps(['modelValue']);
  const emit = defineEmits(['update:modelValue']);
  
  // Internal reactive state
  const panaadhar = ref(props.modelValue || '');
  
  // Allow only A–Z and 0–9 keypresses
  const allowAlphanumeric = (event) => {
    const char = event.key.toUpperCase();
    const regex = /^[A-Z0-9]$/;
    if (!regex.test(char)) {
      event.preventDefault();
    }
  };
  
  // Format input: uppercase, remove invalid characters, max 10 length
  const formatInput = () => {
    panaadhar.value = panaadhar.value.toUpperCase().replace(/[^A-Z0-9]/g, '').slice(0, 12);
  };
  
  // Sync internal value to parent via v-model
  watch(panaadhar, (newValue) => {
    emit('update:modelValue', newValue);
  });
  </script>
  