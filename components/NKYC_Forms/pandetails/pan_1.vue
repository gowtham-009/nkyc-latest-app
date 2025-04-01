<template>
    <div class="primary_color" v-if="contentbox">
        <div class="flex justify-between primary_color items-center px-3"
            :style="{ height: deviceHeight * 0.08 + 'px' }">
            <span class="text-white cursor-pointer" @click="back()"><i class="pi pi-angle-left text-3xl"></i></span>
            <ThemeSwitch />
        </div>
        <div class="flex justify-between px-3 p-1 flex-col bg-white rounded-t-3xl dark:bg-black"
            :style="{ height: deviceHeight * 0.92 + 'px' }">
            <div class="w-full mt-4 px-2">
                <p class="text-4xl text-blue-900 font-bold dark:text-gray-400">
                    Upload Pan card
                </p>
                <p class="text-gray-500 leading-6 font-bold text-xl mt-3">
                    Click a photo of your PAN card or upload from files
                </p>

                <div class="w-full mt-3 rounded-lg px-3 py-3 bg-blue-50 dark:bg-slate-900">
                    <h2 class="text-blue-900 text-2xl font-bold mt-3 dark:text-gray-400">Please remember:</h2>

                    <div class="w-full flex  gap-3 mt-2">
                        <div
                            class="bg-blue-200 px-2 py-1 rounded-lg flex items-center justify-center w-12 h-12 dark:bg-gray-800">
                            <span><i class="text-3xl text-blue-900 pi pi-id-card"></i></span>
                        </div>
                        <div class="p-2">
                            <p class="text-gray-500 leading-6 font-bold text-lg">
                                Upload only the front-side of your PAN card.
                            </p>
                        </div>
                    </div>

                    <div class="w-full flex  gap-3 mt-2">
                        <div
                            class="bg-blue-200 px-1 py-1 rounded-lg flex items-center justify-center w-12 h-12 dark:bg-gray-800">
                            <span><i class="text-3xl text-blue-900 pi pi-image"></i></span>
                        </div>
                        <div class="p-2">
                            <p class="text-gray-500 leading-6 font-bold text-lg">
                                Photo size must not exceed 5MB each.
                            </p>
                        </div>
                    </div>
                    <div class="w-full flex gap-3 mt-2">
                        <div
                            class="bg-blue-200 px-1 py-1 rounded-lg flex items-center justify-center w-12 h-12 dark:bg-gray-800">
                            <span><i class="text-3xl text-blue-900 pi pi-star"></i></span>
                        </div>
                        <div class="p-2">
                            <p class="text-gray-500 leading-6 font-bold text-lg">
                                Photo must be well-lit and glare-free.
                            </p>
                        </div>
                    </div>
                    <div class="w-full flex gap-3 mt-2">
                        <div
                            class="bg-blue-200 px-1 py-1 rounded-lg flex items-center justify-center w-12 h-12 dark:bg-gray-800">
                            <span><i class="text-3xl text-blue-900 pi pi-image"></i></span>
                        </div>
                        <div class="p-2">
                            <p class="text-gray-500 leading-6 font-bold text-lg">
                                Photo must be Clear.
                            </p>
                        </div>
                    </div>
                </div>

            </div>

            <div class="w-full p-1" label="Continue">
                <Button type="button" label="Continue" @click="visibleBottom = true"
                    class=" primary_color wave-btn text-white w-full py-4 text-xl border-0  ">
                </Button>
            </div>

        </div>
    </div>

    <div class="w-full p-2" v-if="camerabox">
        <div v-if="showCamera" class="fixed inset-0 bg-black flex items-center justify-center">
            <video ref="videoRef" autoplay class="w-full h-full object-cover"></video>
            
            <!-- Close Button at Top Left -->

            <Button type="button" icon="pi pi-angle-left"  @click="stopCamera"
            class="absolute bg-gray-50 top-4 left-4 text-black border-0 p-2 rounded  ">
        </Button>
           
            
            <!-- Four Edge Frames -->
            <div class="absolute inset-0  flex justify-between items-center px-5" style="top: -43%;">
                <div class="w-12 h-12 border-4 border-blue-900 border-b-0 border-r-0"></div>
                <div class="w-12 h-12 border-4 border-blue-900 border-b-0 border-l-0"></div>
            </div>
            <div class="absolute inset-0 flex justify-between items-end pb-20 px-5" style="bottom: 24%;">
                <div class="w-12 h-12 border-4 border-blue-900 border-t-0 border-r-0"></div>
                <div class="w-12 h-12 border-4 border-blue-900 border-t-0 border-l-0"></div>
            </div>
            
            <!-- Click Photo Button at Bottom Center -->
            <div class="absolute bottom-10 w-full flex justify-center">
                <Button type="button" label="Click Photo" class="primary_color wave-btn text-white px-20 py-4 text-xl border-0">
                </Button>
            </div>
        </div>
    </div>

    <Drawer v-model:visible="visibleBottom" class="rounded-t-3xl" position="bottom" style="height: auto">
        <Button type="button" label="Open Camera" @click="cameraopen"
            class=" primary_color wave-btn text-white w-full py-4 text-xl border-0  ">
        </Button>
        <p class="text-center font-bold text-blue-600 mt-3 text-2xl">Upload from gallery</p>
    </Drawer>
</template>

<script setup>
import ThemeSwitch from '~/components/darkmode/darkmode.vue'

import { ref, onMounted, onBeforeUnmount } from 'vue';
const deviceHeight = ref(0);
const visibleBottom = ref(false);
const contentbox = ref(true)
const camerabox = ref(false)
onMounted(() => {
    deviceHeight.value = window.innerHeight;
    window.addEventListener('resize', () => {
        deviceHeight.value = window.innerHeight;
    });





});



const back = () => {
    emit('updateDiv', 'div1');
}

const showCamera = ref(false);
const videoRef = ref(null);
let stream = null;


const cameraopen = async () => {
    showCamera.value = true;
    contentbox.value = false;
    camerabox.value = true;
    visibleBottom.value = false;
    try {
        stream = await navigator.mediaDevices.getUserMedia({
            video: { facingMode: "environment" },
        });
        if (videoRef.value) {
            videoRef.value.srcObject = stream;
        }
    } catch (error) {
        console.error("Error accessing the camera:", error);
        showCamera.value = false;
    }
};

const stopCamera = () => {
    if (stream) {
        stream.getTracks().forEach(track => track.stop());
    }
    showCamera.value = false;
    contentbox.value = true;
    camerabox.value = false;
};

onBeforeUnmount(() => {
    stopCamera();
});
</script>

<style>
.p-button-text.p-button-secondary {
    display: none !important;
}
</style>