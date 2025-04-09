<template>
  <div class="flex gap-3">
    <InputText
      type="text"
      class="w-16 font-normal"
      v-model="countryphonenocode"
      disabled
    />

    <InputText
      id="mobile"
      class="w-full font-normal"
      v-model="localPhoneNo"
      inputmode="numeric"
      type="text" 
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

// Keep only numbers and limit to 10 digits
const validateInput = (e) => {
  let value = e.target.value.replace(/\D/g, '').slice(0, 10);
  localPhoneNo.value = value;
  e.target.value = value;
};

watch(localPhoneNo, (newValue) => {
  emit('update:modelValue', newValue);
});
</script>
