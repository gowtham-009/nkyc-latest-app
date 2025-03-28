<template>
    <div class="flex items-center gap-3">
      <Checkbox class="bg-blue-500 " inputId="ingredient1" v-model="checked" binary   size="large"/>
      <label for="ingredient1" class="leading-6 dark:text-slate-200 text-lg font-medium text-slate-500"> I agree to receive communications on my mobile number registered with Ventura </label>
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
  