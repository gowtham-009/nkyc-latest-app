<template>
    <div class="flex items-center gap-2">
      <Checkbox inputId="ingredient1" v-model="checked" binary />
      <label for="ingredient1"> I agreed to open account </label>
    </div>
  </template>
  
  <script setup>
  import { ref, defineProps, defineEmits, watch } from 'vue';
  
  const props = defineProps(['modelValue']);
  const emit = defineEmits(['update:modelValue']);
  
  const checked = ref(props.modelValue);
  
  watch(checked, (newVal) => {
    emit('update:modelValue', newVal);
  });
  </script>
  