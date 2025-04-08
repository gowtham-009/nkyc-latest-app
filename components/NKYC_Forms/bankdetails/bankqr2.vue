<template>
    <div class="primary_color">
        <div class="flex justify-between primary_color items-center px-3"
            :style="{ height: deviceHeight * 0.08 + 'px' }">
            <span @click="back()" class="text-white cursor-pointer">
                <i class="pi pi-angle-left text-3xl"></i>
            </span>
            <ThemeSwitch />
        </div>

        <div class="flex justify-between px-3 p-1 flex-col bg-white rounded-t-3xl dark:bg-black"
            :style="{ height: deviceHeight * 0.92 + 'px' }">
            <div class="w-full mt-4 px-2">
                <p class="text-2xl text-blue-900 font-medium dark:text-gray-400">
                    Link your bank account
                </p>
                <p class="text-md mt-3 text-gray-500 font-medium leading-6">
                    Scan with a UPI app to proceed
                </p>
            </div>

            <div class="w-full flex flex-col items-center py-2 rounded-lg bg-gray-200 p-1 dark:bg-gray-900">
                <div class="w-2/3">
                    <img src="https://cdn.pixabay.com/photo/2013/07/12/14/45/qr-code-148732_1280.png" alt="QR Code">
                </div>
                <!-- Timer Display -->
                <h2 class="font-medium mt-3 text-blue-600 text-xl">
                    {{ formattedTime }}
                </h2>
            </div>

            <div class="w-full flex justify-center p-1">
                <div class="w-3/4 flex gap-2 bg-gray-50 px-2 py-3 rounded-t-3xl dark:bg-gray-900">
                    <p><i class="pi pi-star-fill text-blue-600"></i></p>
                    <p class="text-md leading-6 text-gray-500 font-medium text-left">
                        ₹1 will be debited to verify your bank account and refunded within 48 working hours
                    </p>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue';
import ThemeSwitch from '~/components/darkmode/darkmode.vue';
const emit=defineEmits(['updateDiv']);
const deviceHeight = ref(window.innerHeight);
const timeLeft = ref(300); // 5 minutes = 300 seconds
let timer = null;

// Computed property to format time as MM:SS (e.g., 5:00, 4:59, 4:58)
const formattedTime = computed(() => {
    const minutes = Math.floor(timeLeft.value / 60);
    const seconds = timeLeft.value % 60;
    return `${minutes}:${seconds.toString().padStart(2, '0')}`;
});

// Function to update device height on window resize
const updateHeight = () => {
    deviceHeight.value = window.innerHeight;
};

onMounted(() => {
    window.addEventListener('resize', updateHeight);

    timer = setInterval(() => {
        if (timeLeft.value > 0) {
            timeLeft.value--;
        } else {
            clearInterval(timer);
        }
    }, 1000);
});

onUnmounted(() => {
    clearInterval(timer);
    window.removeEventListener('resize', updateHeight);
});

const back = () => {
    
    emit('updateDiv', 'bank1');
};
</script>
