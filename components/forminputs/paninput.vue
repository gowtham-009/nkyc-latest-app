<template>
    <div class="w-full">
      <label for="" class="text-gray-600 text-lg font-normal">PAN</label>
        <InputText
          id="pan_label"
          class="w-full py-2"
          v-model="pan"
          variant="filled"
          @input="formatInput"
          @keypress="allowAlphanumeric"
          maxlength="10"
          size="large"
          placeholder="AGMLS6667Z"
          
        />
 
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
  