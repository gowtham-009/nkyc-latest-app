<template>
  <div class="primary_color">
    <!-- Box 1 -->
    <div
      class="w-full p-2 primary_color transition-all duration-1000"
      :style="{ height: box1Height + 'px' }"
    >
      <div class="w-full px-2 py-2 flex justify-end items-center">
        <!-- Optional header content -->
      </div>
      <div class="w-full flex justify-center mt-10">
        <span class="text-white" style="font-size: 3rem;">NKYC</span>
      </div>
    </div>

    <!-- Box 2 -->
    <div
      v-if="showBox2"
      class="w-full p-2 flex justify-between flex-col bg-white rounded-t-3xl dark:bg-black transition-opacity duration-1000"
      :style="{ height: deviceHeight * 0.7 + 'px' }"
    >
      <div class="w-full mt-3 px-3 flex flex-col justify-between bg-white">
        <!-- Add your form elements or other content here -->
      </div>
      <div class="w-full">
        <!-- Add buttons or other UI here -->
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const emit = defineEmits(['updateDiv']);
const mobileNumber = ref('');
const checkboxValue = ref('');
const isAnimating = ref(false);
const buttonText = ref('Continue');

const deviceHeight = ref(0);
const box1Height = ref(0);
const showBox2 = ref(false);

onMounted(() => {
  deviceHeight.value = window.innerHeight;
  box1Height.value = deviceHeight.value;

  // Listen for window resize to update values
  window.addEventListener('resize', () => {
    deviceHeight.value = window.innerHeight;
    box1Height.value = showBox2.value ? deviceHeight.value * 0.3 : deviceHeight.value;
  });

  // Trigger transition after 2 seconds
  setTimeout(() => {
    box1Height.value = deviceHeight.value * 0.3;
    showBox2.value = true;
  }, 2000);
});

const handleButtonClick = () => {
  isAnimating.value = true;
  setTimeout(() => {
    isAnimating.value = false;
    emit('updateDiv', 'div2', mobileNumber.value);
  }, 800);
};
</script>

<style scoped>
/* Optional additional styling */
</style>
