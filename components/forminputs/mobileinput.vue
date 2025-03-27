<template>
  <div>
    <IftaLabel>
      <InputText
        id="mobile"
        class="w-full"
        v-model="localPhoneNo"
        variant="filled"
        @keypress="allowOnlyNumbers"
        @input="validateInput"
      />
      <label for="mobile">Phone no*</label>
    </IftaLabel>
  </div>
</template>

<script setup>
import { ref, watch } from 'vue';

const props = defineProps(['modelValue']);
const emit = defineEmits(['update:modelValue']);

const localPhoneNo = ref(props.modelValue || '');

// Allow only number input using keypress
const allowOnlyNumbers = (e) => {
  const charCode = e.which || e.keyCode;
  // Allow: backspace, delete, tab, escape, enter, and numbers
  if (
    charCode !== 8 && // Backspace
    charCode !== 9 && // Tab
    charCode !== 27 && // Escape
    charCode !== 13 && // Enter
    (charCode < 48 || charCode > 57) // Not a number
  ) {
    e.preventDefault();
  }
};

// Validate and limit to 10 digits
const validateInput = () => {
  localPhoneNo.value = localPhoneNo.value.replace(/\D/g, '').slice(0, 10);
};

// Watch for changes in localPhoneNo and emit the updated value
watch(localPhoneNo, (newValue) => {
  emit('update:modelValue', newValue);
});
</script>