<template>
  <div>
    <IftaLabel>
      <InputText
        id="mobile"
        class="w-full"
        v-model="localPhoneNo"
        variant="filled"
        @keydown="allowOnlyNumbers"
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

const allowOnlyNumbers = (e) => {
  // Allow only numbers, backspace, arrow keys, and delete
  if (!/^\d$/.test(e.key) && !['Backspace', 'ArrowLeft', 'ArrowRight', 'Delete'].includes(e.key)) {
    e.preventDefault();
  }

  // Prevent input if the length exceeds 10 characters
  if (localPhoneNo.value.length >= 10 && !['Backspace', 'ArrowLeft', 'ArrowRight', 'Delete'].includes(e.key)) {
    e.preventDefault();
  }
};

// Watch for changes and emit the value
watch(localPhoneNo, (newValue) => {
  emit('update:modelValue', newValue);
});
</script>
