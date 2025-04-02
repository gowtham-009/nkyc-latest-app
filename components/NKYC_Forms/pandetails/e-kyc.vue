<template>
    <div class="primary_color">
        <div class="flex justify-between primary_color items-center px-3"
            :style="{ height: deviceHeight * 0.08 + 'px' }">
            <span @click="back()" class="text-white cursor-pointer"><i class="pi pi-angle-left text-3xl"></i></span>
            <ThemeSwitch />
        </div>
        <div class="flex justify-between px-3 p-1 flex-col bg-white rounded-t-3xl dark:bg-black"
            :style="{ height: deviceHeight * 0.92 + 'px' }">
            <div class="w-full mt-4 px-2">
                <p class="text-4xl text-blue-900 font-bold dark:text-gray-400">
                    Complete your e-KYC
                </p>
                <p class="text-gray-500 leading-5 mt-3 font-medium text-lg">
                    Make sure your mobile number is linked to your Aadhaar card.
                </p>

                <li class="list-none mt-2"><a href="" class="text-blue-900 font-bold text-lg underline">How to link
                        Aadhaar with mobile?</a></li>


                <div class="w-full mt-3 px-2 py-2 rounded-lg bg-gray-100 dark:bg-gray-900">


                    <div class="w-full flex items-center gap-3 p-1 mt-2">
                        <div  class="p-2 px-2 flex justify-center items-center static w-12 h-12 bg-gray-200 rounded-md flex-shrink-0 dark:bg-gray-800">
                            <span><i class="pi pi-file-arrow-up text-2xl text-blue-600"></i></span>
                        </div>
                        <div class="p-2">
                            <p class="font-bold leading-5 text-lg text-gray-500">
                                You will be redirected to Digilocker for e-KYC.
                            </p>
                        </div>
                    </div>

                    <div class="w-full flex items-center gap-3 p-1 mt-2">
                        <div  class="p-2 px-2 flex justify-center items-center static w-12 h-12 bg-gray-200 rounded-md flex-shrink-0 dark:bg-gray-800">
                            <span><i class="pi pi-users text-2xl text-blue-600"></i></span>
                        </div>
                        <div class="p-2">
                            <p class="font-bold leading-5 text-lg text-gray-500">
                                It is a Govt of India initiative with more than 176.75 million trusted users.
                            </p>
                        </div>
                    </div>

                    <div class="w-full flex items-center gap-3 p-1 mt-2">
                        <div
                            class="p-2 px-2 flex justify-center items-center static w-12 h-12 bg-gray-200 rounded-md flex-shrink-0 dark:bg-gray-800">
                            <span><i class="pi pi-id-card text-2xl text-blue-600"></i></span>
                        </div>
                        <div class="p-2">
                            <p class="font-bold leading-5 text-lg text-gray-500">
                                You won't need to enter your details manually as the required documents will be fetched
                                from Digilocker.
                            </p>
                        </div>
                    </div>
                </div>


            </div>

            <div class="w-full p-1" >
                <Button type="button"  @click="handleButtonClick"
                    class=" primary_color wave-btn text-white w-full py-4 text-xl border-0  ">
                    {{ buttonText }}
                    <span v-if="isAnimating" class="wave"></span>
                </Button>
            </div>


        </div>

    </div>
</template>
<script setup>
import ThemeSwitch from '~/components/darkmode/darkmode.vue'
import { ref, onMounted } from 'vue';

const deviceHeight = ref(0);
const isAnimating = ref(false);
const buttonText = ref("Start e-KYC");
onMounted(() => {
    deviceHeight.value = window.innerHeight;
    window.addEventListener('resize', () => {
        deviceHeight.value = window.innerHeight;
    });
});




const emit = defineEmits(['updateDiv']);
const back = () => {

    emit('updateDiv', 'div2');
}


const handleButtonClick = () => {
 isAnimating.value = true;
    setTimeout(() => {
      isAnimating.value = false;
      emit('updateDiv', 'div5');
    }, 800); 
};







</script>
