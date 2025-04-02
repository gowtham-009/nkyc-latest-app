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
                <p class="text-blue-500 font-bold text-2xl text-center">Meri Pehchaan</p>
                <p class="text-center mt-2 leading-6 text-black font-bold text-2xl dark:text-gray-400">
                    You are already registered with DigiLocker. 
                </p>

                <p class="mt-3 text-justify  text-gray-500 text-xl">
                Please enter your 6 digit DigiLocker Security PIN
                </p>

                <div class="w-full mt-2">
                    <Digipin />
                </div>

                <div class="w-full mt-3">
                    <p class="text-blue-600 text-xl dark:text-gray-400">
                      Forget security PIN?
                    </p>
                </div>

             

                <div class="w-full p-1 mt-4">
                <Button type="button" @click="handleButtonClick"
                    class=" primary_color wave-btn text-white w-full py-4 text-xl border-0  ">
                    {{ buttonText }}
                    <span v-if="isAnimating" class="wave"></span>
                </Button>
            </div>

            <div class="w-full p-1 mt-3">
             <p class="text-center leading-5 text-blue-600 text-lg">
                Return to Ventura Securities Onboarding
             </p>
            </div>
            </div>

           


        </div>

    </div>
</template>
<script setup>
import ThemeSwitch from '~/components/darkmode/darkmode.vue'
import { ref, onMounted } from 'vue';
import Digipin from '~/components/forminputs/sixd_pin.vue'

const deviceHeight = ref(0);
const isAnimating = ref(false);
const buttonText = ref("Continue");
onMounted(() => {
    deviceHeight.value = window.innerHeight;
    window.addEventListener('resize', () => {
        deviceHeight.value = window.innerHeight;
    });
});




const emit = defineEmits(['updateDiv']);
const back = () => {

    emit('updateDiv', 'div6');
}









</script>
