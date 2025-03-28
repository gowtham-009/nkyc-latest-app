<template>
  <div class="flex gap-3">
    <InputText type="text"  class="w-16 font-bold" v-model="countryphonenocode" disabled/>
    <FloatLabel variant="in" class="w-full">
      <InputText
        id="mobile"
        class="w-full font-bold"
        v-model="localPhoneNo"
        variant="filled"
        inputmode="numeric"
        type="number"
       
        @input="validateInput"
       
      />
      <label for="mobile" class="dark:text-gray-100">Mobile no*</label>
    </FloatLabel>
  </div>
</template>

<script setup>
import { ref, watch } from 'vue';
const countryphonenocode=ref('+91')
const props = defineProps(['modelValue']);
const emit = defineEmits(['update:modelValue']);

const localPhoneNo = ref(props.modelValue || '');

// Validate input: Allow only numbers and restrict to 10 digits
const validateInput = (e) => {
  const value = e.target.value.replace(/\D/g, ''); // Remove non-numeric characters
  if (value.length > 10) {
    e.target.value = value.slice(0, 10); // Limit to 10 digits
    localPhoneNo.value = e.target.value;
  } else {
    localPhoneNo.value = value;
  }
};

watch(localPhoneNo, (newValue) => {
  emit('update:modelValue', newValue);
});
</script>
