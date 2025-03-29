<template>
  <div class="primary_color">
    <div class="w-full p-2 primary_color"
      :style="{ height: deviceHeight * 0.30 + 'px' }">
     <div class="w-full px-2 py-2 flex justify-between items-center">
      <Button  class="bg-slate-100 border-0 text-slate-600 py-3 dark:bg-black"><i class="pi pi-angle-left text-xl dark:text-gray-500"></i></Button>
      <ThemeSwitch/>
     </div>
   <div class="w-full flex justify-center mt-10 ">
    <span class="text-white" style="font-size: 3rem;">NKYC</span>
   </div>
    </div>

    <div class="w-full p-2 flex flex-col justify-between  bg-white rounded-t-3xl dark:bg-black" 
      :style="{ height: deviceHeight * 0.70 + 'px' }">

    <div class="w-full mt-3 px-3 flex flex-col justify-between" >
     <div class="w-full">
      <p class="text-3xl font-bold dark:text-gray-400">Ready to get started?</p>
      <p class="mt-2 leading-6 text-xl font-semibold text-gray-500">Enter your number to help us set up your investment account</p>
     </div>

      <div class="w-full mt-4">
        <MobileInput v-model="mobileNumber"/>
      </div>

      <div class="w-full mt-4">
        <Checkbox v-model="checkboxValue"/>
      </div>

      <div class="w-full mt-4">
       <p class="text-md text-center text-gray-500">By processing, you accept Venture's <span class="font-semibold">Terms of Use</span> and <span class="font-semibold">Privacy Policy</span></p>
      </div>

    </div>
    <div class="w-full ">
   

      <Button
    type="button"
    label="Continue"
    :disabled="!mobileNumber || !checkboxValue ||  mobileNumber.length !== 10"
    class="primary_color text-white w-full py-4 text-xl border-0 relative overflow-hidden"
    @click="mobile_signup"
  >
    <transition name="fade">
      <span v-if="!isLoading">Continue</span>
    </transition>

    <transition name="fade">
      <span v-if="isLoading" class="loading-text flex items-center relative">
        Progress...
        <span class="loading-wave"></span>
      </span>
    </transition>
  </Button>
      </div>
    </div>
  </div>
</template>

<script setup>

import { ref, onMounted } from 'vue';
import ThemeSwitch from '~/components/darkmode/darkmode.vue'
import MobileInput from '~/components/forminputs/mobileinput.vue'
import Checkbox from '~/components/forminputs/remembercheckbox.vue'
import Button from 'primevue/button';
const emit = defineEmits(['updateDiv']);
const mobileNumber=ref('')
const checkboxValue=ref('')
const isLoading = ref(false)

const deviceHeight = ref(0);
onMounted(() => {
  deviceHeight.value = window.innerHeight;
  window.addEventListener('resize', () => {
    deviceHeight.value = window.innerHeight;

  });
});

const mobile_signup=()=>{
  isLoading.value = true;

  setTimeout(() => {
    isLoading.value = false;
    emit('updateDiv', 'div2', mobileNumber.value);
  },1000);


}


</script>
<style scoped>
/* Smooth Fade Transition */
.fade-enter-active, .fade-leave-active {
  transition: opacity 0.5s ease-in-out;
}
.fade-enter, .fade-leave-to {
  opacity: 0;
}

/* Hover Wave Effect */
.loading-wave {
  position: absolute;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  background: rgba(255, 255, 255, 0.2);
  transform: translateX(-100%);
  animation: waveHover 1.5s ease-in-out infinite;
}

@keyframes waveHover {
  0% {
    transform: translateX(-100%);
  }
  50% {
    transform: translateX(0);
  }
  100% {
    transform: translateX(100%);
  }
}
</style>