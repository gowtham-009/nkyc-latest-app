<template>
    <div class="primary_color">
        <div class="flex justify-between primary_color items-center px-3"
            :style="{ height: deviceHeight * 0.08 + 'px' }">
            <span @click="back()" class="text-white cursor-pointer"><i class="pi pi-angle-left text-3xl"></i></span>
            <ThemeSwitch />
        </div>
        <div class="flex justify-between px-3 p-1 flex-col bg-white rounded-t-3xl dark:bg-black"
            :style="{ height: deviceHeight * 0.92 + 'px' }">
            <div class="w-full mt-2 px-2">
                <p class="text-blue-500 font-medium text-2xl text-center">Meri Pehchaan</p>
                <p class="text-center mt-2 leading-6 text-black font-medium text-2xl dark:text-gray-400">
                    Ventura Securities Onboarding
                </p>

                <p class="mt-1 text-justify font-normal  text-gray-500 text-md">
                    You are about to link your DigiLocker account with Ventura Securities Onboarding application of
                    Ventura Securities Ltd.. You will be signed up for DigiLocker account if it does not exist.
                </p>

                <div class="w-full mt-2">
                    <Aadharno />
                </div>

                <div class="w-full mt-2">
                    <p class="text-gray-600 font-normal text-md">
                        Please enter the following text in the box below:
                    </p>
                </div>

                <div class="w-full flex gap-2 mt-1">
                    <div class="w-full text-gray-400 flex justify-center items-center" style="border: 1px solid gray;">
                        vdfovjsdo
                    </div>
                    <div class="w-full">
                        <captcha/>
                    </div>
                </div>

                <p class="text-gray-500 text-md font-normal text-center mt-2">Unable to read the above image? <span class="text-blue-600">Try another!</span></p>

                <div class="w-full p-1 mt-2">
                <Button type="button" @click="handleButtonClick"
                    class=" primary_color wave-btn text-white w-full py-4 text-xl border-0  ">
                    {{ buttonText }}
                    <span v-if="isAnimating" class="wave"></span>
                </Button>
            </div>
            </div>

            <div class="w-full p-1">
             <p class="text-center font-normal leading-5 text-blue-600 text-md">
                Return to Ventura Securities Onboarding
             </p>
            </div>


        </div>

    </div>
</template>
<script setup>
import ThemeSwitch from '~/components/darkmode/darkmode.vue'
import { ref, onMounted } from 'vue';
import Aadharno from '~/components/forminputs/aadharinput.vue'
import captcha from '~/components/forminputs/cinput.vue'

const deviceHeight = ref(0);
const isAnimating = ref(false);
const buttonText = ref("Next");
onMounted(() => {
    deviceHeight.value = window.innerHeight;
    window.addEventListener('resize', () => {
        deviceHeight.value = window.innerHeight;
    });
});




const emit = defineEmits(['updateDiv']);
const back = () => {

    emit('updateDiv', 'div4');
}

const handleButtonClick=()=>{
    isAnimating.value = true;
    setTimeout(() => {
      isAnimating.value = false;
      emit('updateDiv', 'div6');
    }, 800); 
}







</script>
