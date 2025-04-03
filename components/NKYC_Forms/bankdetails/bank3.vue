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
                <p class="text-4xl text-blue-900 font-medium dark:text-gray-400">
                    Payment in process
                </p>
                <p class="text-xl mt-3 text-gray-500 font-normal leading-6">
                    Open you UPI app to approve the payment request
                </p>
            </div>

            <div class="w-full flex flex-col items-center py-2 rounded-lg bg-gray-200 p-1 dark:bg-gray-900">

                <div class="card flex justify-center">
                    <Knob v-model="minutesLeft" :size="200" :min="0" :max="5" :step="0.01" />
                </div>

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
const emit = defineEmits(['updateDiv']);
const deviceHeight = ref(window.innerHeight);



// Function to update device height on window resize
const updateHeight = () => {
    deviceHeight.value = window.innerHeight;
};

const minutesLeft = ref(5.00); // Start from 5.00 minutes
let timer = null;

const startTimer = () => {
  timer = setInterval(() => {
    if (minutesLeft.value > 0) {
      minutesLeft.value = Math.max(0, (minutesLeft.value - 0.01)).toFixed(2); // Ensure it's formatted properly
      minutesLeft.value = parseFloat(minutesLeft.value); // Convert back to number
    } else {
      clearInterval(timer);
    }
  }, 600); // 600ms = 0.01 minute
};

onMounted(() => {
    window.addEventListener('resize', updateHeight);
    startTimer();

    setTimeout(() => {
        emit('updateDiv', 'bank4');
    }, 3000); // Stop the timer after 5 minutes

});

onUnmounted(() => {

    window.removeEventListener('resize', updateHeight);
    if (timer) clearInterval(timer);
});

const back = () => {

    emit('updateDiv', 'bank1');
};
</script>
