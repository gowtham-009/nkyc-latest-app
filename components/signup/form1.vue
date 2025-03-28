<template>
  <div class="bg-blue-600">
    <div class="w-full p-2 bg-blue-600"
      :style="{ height: deviceHeight * 0.40 + 'px' }">
     <div class="w-full px-2 py-2 flex justify-between items-center">
      <Button  class="bg-slate-100 border-0 text-slate-600 py-3"><i class="pi pi-angle-left text-xl"></i></Button>
      <ThemeSwitch/>
     </div>
   <div class="w-full flex justify-center mt-10 ">
    <span class="text-white" style="font-size: 3rem;">NKYC</span>
   </div>
    </div>

    <div class="w-full p-2 flex flex-col justify-between  bg-white rounded-t-3xl dark:bg-black" 
      :style="{ height: deviceHeight * 0.60 + 'px' }">

    <div class="w-full mt-3 px-3 flex flex-col justify-between" >
     <div class="w-full">
      <p class="text-3xl font-bold">Ready to get started?</p>
      <p class="mt-2 leading-6 text-md font-semibold text-gray-500">Enter your number to help us set up your investment account</p>
     </div>

      <div class="w-full mt-4">
        <MobileInput/>
      </div>

      <div class="w-full mt-4">
        <Checkbox/>
      </div>

      <div class="w-full mt-4">
       <p class="text-md text-center text-gray-500">By processing, you accept Venture's <span class="font-semibold">Terms of Use</span> and <span class="font-semibold">Privacy Policy</span></p>
      </div>

    </div>
    <div class="w-full ">
      <Button label="Continue" class="bg-blue-600 w-full py-4 text-xl " size="large"/>
      </div>
    </div>
  </div>
</template>

<script setup>

import { ref, onMounted } from 'vue';
import ThemeSwitch from '~/components/darkmode/darkmode.vue'
import MobileInput from '~/components/forminputs/mobileinput.vue'
import Checkbox from '~/components/forminputs/remembercheckbox.vue'



const deviceHeight = ref(0);
onMounted(() => {
  deviceHeight.value = window.innerHeight;
  window.addEventListener('resize', () => {
    deviceHeight.value = window.innerHeight;

  });
});




</script>
<style>

</style>
