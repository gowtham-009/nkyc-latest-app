<template>
  <div class="flex gap-3">
    <InputText type="text" class="w-16 font-bold" v-model="countryphonenocode" disabled />
    
    <InputText
      id="mobile"
      class="w-full font-bold"
      v-model="localPhoneNo"
      inputmode="numeric"
      type="number"
      placeholder="Enter Phone Number"
      @input="validateInput"
      maxlength="10"
    />
  </div>
</template>

<script setup>
import { ref, watch } from 'vue';
const countryphonenocode = ref('+91');
const props = defineProps(['modelValue']);
const emit = defineEmits(['update:modelValue']);

const localPhoneNo = ref(props.modelValue || '');

// Validate input: Allow only numbers and restrict to 10 digits
const validateInput = (e) => {
  let value = e.target.value.replace(/\D/g, ''); // Allow only numeric digits
  value = value.slice(0, 10); // Limit to 10 digits
  localPhoneNo.value = value;
  e.target.value = value;
};

watch(localPhoneNo, (newValue) => {
  emit('update:modelValue', newValue);
});
</script>
