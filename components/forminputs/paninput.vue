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
        <label for="pan_label">PAN NO*</label>
      </FloatLabel>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  
  const props = defineProps(['modelValue']);
  const emit = defineEmits(['update:modelValue']);
  
  const pan =  ref(props.modelValue || '');
  
  
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

  watch(pan, (newValue) => {
    emit('update:modelValue', newValue);
  });
  </script>
  