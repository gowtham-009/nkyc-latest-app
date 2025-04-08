<template>
    <div class="primary_color">
        <div class="flex justify-end primary_color items-center px-3"
            :style="{ height: deviceHeight * 0.08 + 'px' }">
            <ThemeSwitch />
        </div>
        <div class="flex justify-between px-3 p-1 flex-col bg-white rounded-t-3xl dark:bg-black" 
            :style="{ height: deviceHeight * 0.92 + 'px' }">
            <div class="w-full mt-4 px-2">
                <p class="text-2xl text-blue-900 font-medium dark:text-gray-400">
                    Take a selfie
                </p>
                <p class="text-gray-500 leading-6 font-normal text-md mt-3">
                    Ensure face appears clearly within the frame
                </p>

                <div class="w-full mt-3 rounded-lg px-3 py-3 bg-blue-50 dark:bg-slate-900">
                    <h2 class="text-blue-900 text-xl font-medium mt-3 dark:text-gray-400">Please remember:</h2>

                    <div class="w-full flex items-center  gap-3 mt-2">
                        <div
                            class="p-2 px-2 flex justify-center items-center  w-10 h-10 bg-gray-200 dark:bg-gray-800 rounded-md flex-shrink-0">
                            <span> <span><i class="pi pi-hourglass text-xl text-blue-600"></i></span></span>
                        </div>
                        <div class="p-2">
                            <p class="text-gray-500 leading-6 font-normal text-md">
                               Avoid hats and glasses.
                            </p>
                        </div>
                    </div>

                    <div class="w-full flex items-center gap-3 mt-2">
                        <div
                        class="p-2 px-2 flex justify-center items-center  w-10 h-10 bg-gray-200 dark:bg-gray-800 rounded-md flex-shrink-0">
                            <span><i class="pi pi-face-smile text-xl text-blue-600"></i></span>
                        </div>
                        <div class="p-2">
                            <p class="text-gray-500 leading-6 font-normal text-md">
                                Keep your face straight
                            </p>
                        </div>
                    </div>
                    <div class="w-full flex items-center gap-3 mt-2">
                        <div
                        class="p-2 px-2 flex justify-center items-center  w-10 h-10 bg-gray-200 dark:bg-gray-800 rounded-md flex-shrink-0">
                        <span><i class="pi pi-sparkles text-xl text-blue-600"></i></span>
                        </div>
                        <div class="p-2">
                            <p class="text-gray-500 leading-6 font-normal text-md">
                               Take a clear picture
                            </p>
                        </div>
                    </div>
                    <div class="w-full flex items-center gap-3 mt-2">
                        <div
                        class="p-2 px-2 flex justify-center items-center  w-10 h-10 bg-gray-200 dark:bg-gray-800 rounded-md flex-shrink-0">
                        <span><i class="pi pi-sun text-xl text-blue-600"></i></span>
                        </div>
                        <div class="p-2">
                            <p class="text-gray-500 leading-6 font-normal text-md">
                               Be in a bright area
                            </p>
                        </div>
                    </div>
                    <div class="w-full flex items-center gap-3 mt-2">
                        <div
                        class="p-2 px-2 flex justify-center items-center  w-10 h-10 bg-gray-200 dark:bg-gray-800 rounded-md flex-shrink-0">
                        <span><i class="pi pi-map-marker text-xl text-blue-600"></i></span>
                        </div>
                        <div class="p-2">
                            <p class="text-gray-500 leading-6 font-normal text-md">
                                Enable location access
                            </p>
                        </div>
                    </div>
                </div>

            </div>

            <div class="w-full p-1">
                <p class="mb-5 text-left text-md text-gray-500 font-normal">
                    These details are required by SEBI to open your Demat account.
                </p>
                <Button type="button"   @click="handleButtonClick"
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
import { ref, onMounted, onBeforeUnmount } from 'vue';

const deviceHeight = ref(0);
const isAnimating = ref(false);
const buttonText = ref("Open camera");

onMounted(() => {
    deviceHeight.value = window.innerHeight;
    window.addEventListener('resize', () => {
        deviceHeight.value = window.innerHeight;
    });
});









const emit = defineEmits(['updateDiv']);
const back = () => {

   // emit('updateDiv', 'div2');
}

const handleButtonClick = () => {
 isAnimating.value = true;
    setTimeout(() => {
      isAnimating.value = false;
      emit('updateDiv', 'takephoto');
    }, 800); 
};




</script>
