<template>
    <div class="w-full">
      <label for="pan_label" class="text-gray-500 text-lg font-normal">Pincode</label>
      <InputText
        id="pan_label"
        class="w-full py-2"
        v-model="Pincode"
        variant="filled"
        @keypress="allowOnlyNumbers"
        @input="formatToNumbersOnly"
        maxlength="12"
        size="large"
        placeholder="000 000"
      />
    </div>
  </template>
  
  <script setup>
  import { ref, watch } from 'vue';
  
  const props = defineProps(['modelValue']);
  const emit = defineEmits(['update:modelValue']);
  
  const Pincode = ref(props.modelValue || '');
  
  // Allow only digits on keypress
  const allowOnlyNumbers = (event) => {
    const char = event.key;
    const regex = /^[0-9]$/;
    if (!regex.test(char)) {
      event.preventDefault();
    }
  };
  
  // Remove any non-digit characters, and limit to 12 digits
  const formatToNumbersOnly = () => {
    Pincode.value = Pincode.value.replace(/[^0-9]/g, '').slice(0, 12);
  };
  
  watch(Pincode, (newValue) => {
    emit('update:modelValue', newValue);
  });
  </script>
  