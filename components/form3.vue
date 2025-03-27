<template>

    <div class="relative bg-indigo-100 dark:bg-indigo-900">
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
                        <span class="text-slate-500 dark:text-slate-300">We have sent an OTP to your Email ID</span> <br>
                        <span class="text-slate-500 dark:text-slate-300">{{ emailID }}</span>
                        <div class="mt-3">
                            <emailotp v-model="e_otp" />
                            <div class="p-1 w-full flex justify-between">
                                <h2 class="font-medium text-lg dark:text-slate-300">00:{{ timeLeft.toString().padStart(2, '0') }}s</h2>
                                <span class="text-indigo-500 cursor-pointer text-xl font-medium dark:text-slate-300">Resend OTP</span>
                            </div>

                            <div class="w-full mt-2">
                                <Button label="Verify OTP" @click="dashboardtrigger()" class="w-full dark:bg-white" severity="info"  :disabled="isButtonDisabled" />
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

import emailotp from '~/components/forminputs/otpinput.vue';


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



const emailID = ref('')



const e_otp = ref('')
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
    const email = props.data.email_id || '';
    const [name, domain] = email.split('@');
    if (name && domain) {
        const maskedName = name.length > 2
            ? `${name.slice(0, 2)}${'*'.repeat(name.length - 2)}`
            : name;
        emailID.value = `${maskedName}@${domain}`;
    } else {
        emailID.value = email;
    }
});

watch(e_otp, (newval) => {
    if (newval.length > 5) {
        visible.value = true
        clearInterval(timer);

    }
})

const isButtonDisabled = computed(() => e_otp.value.length <= 5);

const dashboardtrigger = () => {
    if (e_otp.value.length > 5) {
        alert('go to dashboard')
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
