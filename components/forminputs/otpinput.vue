<template>
  <div class="card flex justify-center">
    <div class="flex flex-col items-center py-2">
      <InputOtp class="w-full"  @input="validateOtp" v-model="otp" :length="6" style="gap: 0">
        <template #default="{ attrs, events }">
          <input  type="text" v-bind="attrs" v-on="events" class="custom-otp-input w-full dark:text-slate-100" />
        </template>
      </InputOtp>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';


const props = defineProps(['modelValue']);
const emit = defineEmits(['update:modelValue']);
const otp =  ref(props.modelValue || '');
function validateOtp() {
  otp.value = otp.value.replace(/\D/g, ''); // Remove non-numeric characters
  }

  watch(otp, (newValue) => {
    emit('update:modelValue', newValue);
  });
</script>

<style scoped>
.custom-otp-input {
 
  height: 48px;
  font-size: 24px;
  appearance: none;
  text-align: center;
  transition: all 0.2s;
  border-radius: 0;
  border: 1px solid rgb(184, 183, 183);
  background: transparent;
  outline-offset: -2px;
  outline-color: transparent;
  transition: outline-color 0.3s;
 
}

.custom-otp-input:focus {
  outline: none;
}

.custom-otp-input:first-child {
  border-top-left-radius: 12px;
  border-bottom-left-radius: 12px;
}

.custom-otp-input:last-child {
  border-top-right-radius: 12px;
  border-bottom-right-radius: 12px;
}
</style>
