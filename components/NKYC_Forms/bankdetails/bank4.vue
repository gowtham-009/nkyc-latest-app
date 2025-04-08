<template>
    <div class="primary_color">
        <div class="flex justify-end primary_color items-center px-3" :style="{ height: deviceHeight * 0.08 + 'px' }">

            <ThemeSwitch />
        </div>
        <div class="flex justify-between px-3 p-1 flex-col bg-white rounded-t-3xl dark:bg-black"
            :style="{ height: deviceHeight * 0.92 + 'px' }">
            <div class="w-full mt-4 px-2">

                <div class="w-full flex justify-center">
                    <img src="https://cdn-icons-png.flaticon.com/128/2830/2830289.png" alt="">
                </div>

                <h1 class="text-center mt-3 text-2xl font-medium text-blue-950 dark:text-gray-400">
                    Bank account added
                </h1>
                <p class="text-md text-center mt-1 font-normal text-gray-500">
                    Your bank details have been verified.
                </p>

                <div class="mt-3 w-full px-2 py-3 bg-gray-100 rounded-lg dark:bg-gray-900">
                    <div class="w-full flex items-center gap-2">
                        <div
                            class="p-2 px-2 flex justify-center items-center static w-14 h-14 bg-blue-200 dark:bg-slate-900  rounded-full  flex-shrink-0">
                            <span><i class="pi pi-building-columns text-blue-900 text-3xl md:text-4xl"></i></span>
                        </div>

                        <div>
                            <p class="text-medium text-lg text-gray-500">Bank Name</p>
                        </div>

                    </div>

                    <div class="w-full flex mt-2 p-1" >
                        <div class="w-full p-1" >
                            <p class="text-md text-left text-gray-500 font-normal">Acc.No.</p>
                        </div>
                        <div class="w-full p-1" >
                            <p class="text-lg text-right text-blue-900 font-medium dark:text-gray-400">XXXXXXXXX134</p>
                        </div>
                    </div>
                    <div class="w-full flex p-1" >
                        <div class="w-full p-1" >
                            <p class="text-md text-left text-gray-500 font-normal">IFSC Code</p>
                        </div>
                        <div class="w-full p-1" >
                            <p class="text-lg text-right text-blue-900 font-medium dark:text-gray-400">IOBXXXXXXX134</p>
                        </div>
                    </div>
                    <div class="w-full flex p-1" >
                        <div class="w-full p-1" >
                            <p class="text-md text-left text-gray-500 font-normal">Branch</p>
                        </div>
                        <div class="w-full p-1" >
                            <p class="text-lg text-right text-blue-900 font-medium dark:text-gray-400">DIGITAL BANKING SERVICE</p>
                        </div>
                    </div>
                </div>
            </div>

            <div class="w-full p-1" >
                <Button type="button"  @click="handleButtonClick" 
                    class=" primary_color wave-btn text-white w-full py-4 text-xl border-0  ">
                    {{ buttontext }}
                    <span v-if="isAnimating" class="wave"></span>
                </Button>
            </div>


        </div>

    </div>






</template>
<script setup>
import ThemeSwitch from '~/components/darkmode/darkmode.vue'
import { ref, onMounted, onBeforeUnmount } from 'vue';

const emit = defineEmits(['updateDiv']);
const deviceHeight = ref(0);
const buttontext =ref('Continue')
const isAnimating = ref(false);
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
      emit('updateDiv', 'submission', '3');
    }, 800); 
};










</script>
