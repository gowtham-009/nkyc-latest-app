<template>
    <div class="primary_color" v-if="contentbox">
        <div class="flex justify-between primary_color items-center px-3"
            :style="{ height: deviceHeight * 0.08 + 'px' }">
            <span @click="back()" class="text-white cursor-pointer"><i class="pi pi-angle-left text-3xl"></i></span>
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
                            class="bg-blue-200 px-2 py-2 rounded-lg flex items-center justify-center w-12 h-12 dark:bg-gray-800">
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
                            class="bg-blue-200 px-2 py-2 rounded-lg flex items-center justify-center w-12 h-12 dark:bg-gray-800">
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
                            class="bg-blue-200 px-2 py-2 rounded-lg flex items-center justify-center w-12 h-12 dark:bg-gray-800">
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
                            class="bg-blue-200 px-2 py-2 rounded-lg flex items-center justify-center w-12 h-12 dark:bg-gray-800">
                            <span><i class="text-3xl text-blue-900 pi pi-image"></i></span>
                        </div>
                        <div class="p-2">
                            <p class="text-gray-500 leading-6 font-bold text-lg">
                                Photo must be clear.
                            </p>
                        </div>
                    </div>
                </div>

            </div>

            <div class="w-full p-1" label="Continue">
                <Button type="button" label="Continue" @click="visibleBottom = true"
                    class=" primary_color wave-btn text-white w-full py-4 text-xl border-0  "></Button>
            </div>

        </div>
    </div>

    <div class="w-full p-2" v-if="camerabox">
        <div v-if="showCamera" class="fixed inset-0 bg-black flex items-center justify-center">
            <video ref="videoRef" autoplay class="w-full h-full object-cover"></video>

            <!-- Canvas for capturing image -->
            <canvas ref="canvasRef" class="hidden"></canvas>

            <!-- Close Button at Top Left -->
            <Button type="button" icon="pi pi-angle-left" @click="backpan()"
                class="absolute bg-gray-50 top-4 left-4 text-black border-0 p-2 rounded" style="z-index: 5;">
            </Button>

            <!-- Four Edge Frames -->
            <div class="absolute inset-0 flex justify-between items-center px-5" style="top: -43%;">
                <div class="w-12 h-12 border-4 border-blue-900 border-b-0 border-r-0"></div>
                <div class="w-12 h-12 border-4 border-blue-900 border-b-0 border-l-0"></div>
            </div>
            <div class="absolute inset-0 flex justify-between items-end pb-20 px-5" style="bottom: 24%;">
                <div class="w-12 h-12 border-4 border-blue-900 border-t-0 border-r-0"></div>
                <div class="w-12 h-12 border-4 border-blue-900 border-t-0 border-l-0"></div>
            </div>

            <!-- Click Photo Button at Bottom Center -->
            <div class="absolute bottom-10 w-full flex justify-center">
                <Button type="button" :label="photoCaptured ? 'Retake' : 'Click Photo'"
                        @click="handleCapture"
                        class="primary_color wave-btn text-white px-20 py-4 text-xl border-0">
                </Button>
            </div>

            <!-- Display Captured Image -->
            <div v-if="photoCaptured" class="absolute bottom-32 w-full flex justify-center">
                <img :src="capturedImage" alt="Captured Image" class="w-full max-w-md"/>
            </div>
        </div>
    </div>

    <Drawer v-model:visible="visibleBottom" class="rounded-t-3xl" position="bottom" style="height: auto">
        <Button type="button" label="Open Camera" @click="cameraopen"
            class=" primary_color wave-btn text-white w-full py-4 text-xl border-0">
        </Button>
        <p class="text-center font-bold text-blue-600 mt-3 text-2xl">Upload from gallery</p>
    </Drawer>
</template>
<script setup>
import ThemeSwitch from '~/components/darkmode/darkmode.vue'
import { ref, onMounted, onBeforeUnmount } from 'vue';

const deviceHeight = ref(0);
const visibleBottom = ref(false);
const contentbox = ref(true);  // Initially showing content box
const camerabox = ref(false);  // Initially not showing camera box
const showCamera = ref(false);
const photoCaptured = ref(false); // To track if the photo is captured
const capturedImage = ref(null); // To store the captured image as a data URL
const videoRef = ref(null);
const canvasRef = ref(null);
let stream = null;

onMounted(() => {
    deviceHeight.value = window.innerHeight;
    window.addEventListener('resize', () => {
        deviceHeight.value = window.innerHeight;
    });
});

const backpan = () => {
 
    stopCamera();

    // Show the content box and hide the camera box
    contentbox.value = true;
    camerabox.value = false;

    // Reset any states related to the camera
    photoCaptured.value = false;
    capturedImage.value = null;
};

const cameraopen = async () => {
    showCamera.value = true;
    contentbox.value = false;
    camerabox.value = true;
    visibleBottom.value = false;
    photoCaptured.value = false;
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
        stream.getTracks().forEach(track => track.stop()); // Stop all tracks
    }
    showCamera.value = false; // Hide the camera
    camerabox.value = false; // Hide the camera box
};

const handleCapture = () => {
   
    if (photoCaptured.value) {
        // If photo is already taken, reopen the camera
        photoCaptured.value = false;
        capturedImage.value = null; // Clear the captured image
        cameraopen();
    } else {
        // Capture the photo
        captureImage();
    }
};

const captureImage = () => {
    if (videoRef.value && canvasRef.value) {
        const video = videoRef.value;
        const canvas = canvasRef.value;
        const ctx = canvas.getContext('2d');
        // Set canvas size to video size
        canvas.width = video.videoWidth;
        canvas.height = video.videoHeight;
        // Draw the current video frame on the canvas
        ctx.drawImage(video, 0, 0, canvas.width, canvas.height);
        // Convert the canvas to an image
        capturedImage.value = canvas.toDataURL('image/jpeg');
        photoCaptured.value = true;
    }
};

onBeforeUnmount(() => {
    stopCamera();
});
const emit = defineEmits(['updateDiv']);
const back=()=>{

    emit('updateDiv', 'div1');
}
</script>
