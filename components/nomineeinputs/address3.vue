<template>
    <div class="w-full">
      <label for="pan_label" class="text-gray-500 text-lg font-normal">Address line 3</label>
      <InputText
        id="pan_label"
        class="w-full py-2"
        v-model="address3"
        variant="filled"
        @input="formatInput"
        @keypress="allowCustomCharacters"
        maxlength="100"
        size="large"
        placeholder="Nominee's address line 3"
      />
    </div>
  </template>
  
  <script setup>
  import { ref, watch } from 'vue';
  
  const props = defineProps(['modelValue']);
  const emit = defineEmits(['update:modelValue']);
  
  const address3 = ref(props.modelValue || '');
  
  // Allow only A-Z, a-z, 0-9, ., /, and space
  const allowCustomCharacters = (event) => {
    const char = event.key;
    const regex = /^[a-zA-Z0-9./\s]$/;
    if (!regex.test(char)) {
      event.preventDefault();
    }
  };
  
  // Format input: convert to uppercase, allow only valid characters, and max 12 length
  const formatInput = () => {
    address3.value = address3.value
      .toUpperCase()
      .replace(/[^A-Z0-9./\s]/g, '')
      .slice(0, 100);
  };
  
  watch(address3, (newValue) => {
    emit('update:modelValue', newValue);
  });
  </script>
  