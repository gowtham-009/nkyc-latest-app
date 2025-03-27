<template>

    <div class=" bg-indigo-100 dark:bg-indigo-900">
        <div class="flex justify-end items-center px-3 bg-indigo-100 dark:bg-indigo-900  "
            :style="{ height: deviceHeight * 0.06 + 'px' }">
            <ThemeSwitch />
        </div>
        <div class="flex bg-indigo-50  rounded-t-3xl dark:bg-indigo-950"
            :style="{ height: deviceHeight * 0.94 + 'px' }">
            <div class="w-1/2 p-2 flex justify-center items-center dk">

            </div>
            <div class="w-1/2 p-3 mt-3 flex items-center md ">
                <!-- mobile-otp -->
                <div class="w-full">
                    <div class="w-full">
                        <h1 class="text-slate-800 font-medium dark:text-slate-200" style="font-size: 1.7rem;">Enter OTP here</h1>
                        <span class="text-slate-500 dark:text-slate-300">We have sent an OTP to your mobile number</span> <br>
                        <span class="text-slate-500 dark:text-slate-300">+91-{{ phoneNumber }}</span>
                        <div class="mt-3">
                            <phoneotp v-model="p_otp"  />
                            <div class="p-1 w-full flex justify-between">
                                <h2 class="font-medium text-lg dark:text-slate-300">00:{{ timeLeft.toString().padStart(2, '0') }}s</h2>
                                <span class="text-indigo-500 cursor-pointer text-xl font-medium dark:text-slate-300">Resend OTP</span>
                            </div>

                            <div class="w-full mt-2">
                                <Button label="Verify OTP" @click="emailotptrigger()" class="w-full dark:bg-white" severity="info"  :disabled="isButtonDisabled"  />
                            </div>
                        </div>
                    </div>
                </div>
            </div>

        </div>


    </div>

    <Dialog v-model:visible="visible" modal header="OTP Status" :style="{ width: '25rem' }">
        <span>Your OTP Successfully Verified</span>
    </Dialog>
</template>

<script setup>

import { ref, onMounted, watch, watchEffect, onUnmounted } from 'vue';

import phoneotp from '~/components/forminputs/otpinput.vue';


import ThemeSwitch from '~/components/darkmode/darkmode.vue'



const visible = ref(false);
const props = defineProps({
    data: {
        type: Object,
        default: () => ({}),
    },
});

const timeLeft = ref(60); // Start from 60 seconds

let timer = null;



const phoneNumber = ref('')




const p_otp = ref('')
const deviceHeight = ref(0);



onMounted(() => {
    deviceHeight.value = window.innerHeight;
    window.addEventListener('resize', () => {
        deviceHeight.value = window.innerHeight;
    });

    timer = setInterval(() => {
        if (timeLeft.value > 0) {
            timeLeft.value -= 1;
        } else {
            clearInterval(timer);
        }
    }, 1000);


});

onUnmounted(() => {
    clearInterval(timer);
});

const emit = defineEmits(['updateDiv']);


watchEffect(() => {
    const mobileNo = props.data.mobile_no || '';
    phoneNumber.value = mobileNo.length >= 10
        ? `${mobileNo.slice(0, 2)}******${mobileNo.slice(-3)}`
        : mobileNo;

   
});

watch(p_otp, (newval) => {
    if (newval.length > 5) {
         visible.value = true
        clearInterval(timer);
    }
})
const isButtonDisabled = computed(() => p_otp.value.length <= 5);

const emailotptrigger = () => {
    if (p_otp.value.length > 5) {
         emit('updateDiv', 'div3', props.data);
    }
};

</script>
<style>
.disabled {
    pointer-events: none;
    opacity: 0.5;
}

@media(max-width:992px) {
    .hd {
        display: none !important;
    }

}
</style>
