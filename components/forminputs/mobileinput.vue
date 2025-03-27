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
  if (charCode < 48 || charCode > 57) {
    e.preventDefault();
  }
};

// Validate and limit to 10 digits
const validateInput = () => {
  localPhoneNo.value = localPhoneNo.value.replace(/\D/g, '').slice(0, 10);
};

watch(localPhoneNo, (newValue) => {
  emit('update:modelValue', newValue);
});
</script>
