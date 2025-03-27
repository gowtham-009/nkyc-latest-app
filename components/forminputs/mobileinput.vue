<template>
  <div>
    <IftaLabel>
      <InputText
        id="mobile"
        class="w-full"
        v-model="localPhoneNo"
        variant="filled"
        inputmode="numeric"
        type="number"
        @input="validateInput"
      />
      <label for="mobile">Mobile no*</label>
    </IftaLabel>
  </div>
</template>

<script setup>
import { ref, watch } from 'vue';

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
