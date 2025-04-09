<template>
  <div class="w-full">
    <label for="pan_label" class="text-gray-600 text-lg font-normal">PAN</label>
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
import { ref, watch } from 'vue';

// Props and Emits for v-model compatibility
const props = defineProps(['modelValue']);
const emit = defineEmits(['update:modelValue']);

// Internal reactive state
const pan = ref(props.modelValue || '');

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
  pan.value = pan.value.toUpperCase().replace(/[^A-Z0-9]/g, '').slice(0, 10);
};

// Sync internal value to parent via v-model
watch(pan, (newValue) => {
  emit('update:modelValue', newValue);
});
</script>
