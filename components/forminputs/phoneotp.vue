<template>
    <div>
        <div class="card flex justify-center">
        <InputOtp v-model="phoneotp"  @input="validateOtp"  size="large"/>
    </div>
    </div>
</template>

<script setup>
import { ref, watch } from 'vue';
const props = defineProps(['modelValue']);
  const emit = defineEmits(['update:modelValue']);

const phoneotp=ref(props.modelValue || '');
function validateOtp() {
    phoneotp.value = phoneotp.value.replace(/\D/g, ''); // Remove non-numeric characters
  }

    // Watch for changes and emit the value
    watch(phoneotp, (newValue) => {
    emit('update:modelValue', newValue);
  });
</script>

<style>

</style>