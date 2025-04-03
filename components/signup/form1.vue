<template>
  <div class="primary_color">
    <div class="w-full p-2 primary_color" :style="{ height: deviceHeight * 0.30 + 'px' }">
      <div class="w-full px-2 py-2 flex justify-between items-center">
        <Button class="bg-slate-100 border-0 text-slate-600 py-3 dark:bg-black">
          <i class="pi pi-angle-left text-xl dark:text-gray-500"></i>
        </Button>
        <ThemeSwitch />
      </div>
      <div class="w-full flex justify-center mt-10 ">
        <span class="text-white" style="font-size: 3rem;">NKYC</span>
      </div>
    </div>

    <div class="w-full p-2 flex flex-col justify-between bg-white rounded-t-3xl dark:bg-black" :style="{ height: deviceHeight * 0.70 + 'px' }">
      <div class="w-full mt-3 px-3 flex flex-col justify-between">
        <div class="w-full">
          <p class="text-3xl font-medium dark:text-gray-400">Ready to get started?</p>
          <p class="mt-2 leading-6 text-xl font-normal text-gray-500">Enter your number to help us set up your investment account</p>
        </div>

        <div class="w-full mt-4">
          <MobileInput v-model="mobileNumber" />
        </div>

        <div class="w-full mt-4">
          <Checkbox v-model="checkboxValue" />
        </div>

        <div class="w-full mt-4">
          <p class="text-md text-center font-normal text-gray-500">
            By processing, you accept Venture's <span class="font-medium">Terms of Use</span> and <span class="font-normal">Privacy Policy</span>
          </p>
        </div>
      </div>
      <div class="w-full">
       
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

const emit = defineEmits(['updateDiv']);
const mobileNumber = ref('');
const checkboxValue = ref('');
const isAnimating = ref(false);
const buttonText = ref("Continue");
const deviceHeight = ref(0);
onMounted(() => {
  deviceHeight.value = window.innerHeight;
  window.addEventListener('resize', () => {
    deviceHeight.value = window.innerHeight;
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

<style>

</style>
