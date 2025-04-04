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
                <p class="text-4xl text-blue-900 font-medium dark:text-gray-400">
                    Take a selfie
                </p>
                <p class="text-lg mt-3 text-gray-500 font-normal leading-6">
                    Ensure your face appears clearly within the frame
                </p>
                <div>
                    <p class="text-lg mt-3 text-gray-500 font-normal leading-6" v-if="latitude && longitude">Latitude: {{ latitude }}, Longitude: {{ longitude }}</p>
                    <p v-if="errorMessage" class="text-red-500">{{ errorMessage }}</p>
                </div>

                <div class="w-full p-1 mt-3 flex justify-center">
                    <CMAIDENTIFY @imageCaptured="handleCapturedImage"/>
                </div>
            </div>

            <div class="w-full p-1">
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
import useGeolocation from '~/composables/useGeolocation'
import CMAIDENTIFY from '~/components/NKYC_Forms/photo&sign/cameraidentification/cmaidentify.vue'
const deviceHeight = ref(0);
const emit = defineEmits(['updateDiv']);
const capturedImageData = ref(null)
const isAnimating = ref(false);
const buttonText = ref("Continue");

const handleCapturedImage = (image) => {
  capturedImageData.value = image
 
}

const { latitude, longitude, errorMessage } = useGeolocation()

onMounted(() => {
    deviceHeight.value = window.innerHeight;
    window.addEventListener('resize', () => {
        deviceHeight.value = window.innerHeight;
    });
});

const back = () => {
    emit('updateDiv', 'photosign1');
};
const handleButtonClick = () => {
  
 isAnimating.value = true;
    setTimeout(() => {
      isAnimating.value = false;
      emit('updateDiv', 'photoproceed', capturedImageData.value);

    }, 800); 
};

</script>
