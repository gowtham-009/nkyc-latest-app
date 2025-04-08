<template>
  <div class="primary_color overflow-hidden h-screen">
    <!-- Box 1 -->
    <div
      class="w-full p-2 primary_color transition-all duration-300"
      :style="{ height: box1Height + 'px' }"
    >
    <div class="w-full px-2 py-2 flex justify-end items-center">
        <ThemeSwitch />
      </div>

      <div class="w-full flex justify-center mt-10">
        <span class="text-white text-5xl">NKYC</span>
      </div>
    </div>

    <!-- Box 2 -->
    <div
      v-show="showBox2"
      class="w-full p-2 flex flex-col justify-between bg-white rounded-t-3xl dark:bg-black transition-all duration-300"
      :style="{ height: box2Height + 'px' }"
    >
    <div class="w-full mt-3 px-3 flex flex-col justify-between">
        <div class="w-full">
          <p class="text-2xl font-medium dark:text-gray-400">Ready to get started?</p>
          <p class="mt-2 leading-6 text-md font-normal text-gray-500">Enter your number to help us set up your investment account</p>
        </div>

        <div class="w-full mt-4">
          <MobileInput v-model="mobileNumber" />
        </div>

        <div class="w-full mt-4">
          <Checkbox v-model="checkboxValue" />
        </div>

       
      </div>
      <div class="w-full">
        <p class="text-md text-center mb-2 font-normal text-gray-500">
            By processing, you accept Venture's <span class="font-medium">Terms of Use</span> and <span class="font-normal">Privacy Policy</span>
          </p>
        <Button
        :disabled="!mobileNumber || !checkboxValue || mobileNumber.length !== 10"
         @click="handleButtonClick" class="primary_color wave-btn w-full text-white  py-4 text-xl border-0">
        {{ buttonText }}
        <span v-if="isAnimating" class="wave"></span>
      </Button>

      </div>

    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import ThemeSwitch from '~/components/darkmode/darkmode.vue';
import MobileInput from '~/components/forminputs/mobileinput.vue';
import Checkbox from '~/components/forminputs/remembercheckbox.vue';
import Button from 'primevue/button';

const box1Height = ref(0);
const box2Height = ref(0);
const showBox2 = ref(false);

const emit = defineEmits(['updateDiv']);
const mobileNumber = ref('');
const checkboxValue = ref('');
const isAnimating = ref(false);
const buttonText = ref("Continue");

onMounted(() => {
  const fullHeight = window.innerHeight;

  // Initial state: full height to box 1, box 2 hidden
  box1Height.value = fullHeight;
  box2Height.value = 0;
  showBox2.value = false;

  // After 2 seconds: show box 2 and animate heights
  setTimeout(() => {
    showBox2.value = true;
    box1Height.value = fullHeight * 0.3;
    box2Height.value = fullHeight * 0.7;
  }, 500);

  // Optional: handle resize
  window.addEventListener('resize', () => {
    const updatedHeight = window.innerHeight;
    if (!showBox2.value) {
      box1Height.value = updatedHeight;
      box2Height.value = 0;
    } else {
      box1Height.value = updatedHeight * 0.3;
      box2Height.value = updatedHeight * 0.7;
    }
  });
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

</style>
