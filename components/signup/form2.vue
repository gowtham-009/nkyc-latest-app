<template>
    <div class="primary_color">
        <div class="flex justify-between primary_color items-center px-3" 
            :style="{ height: deviceHeight * 0.08 + 'px' }">
            <span class="text-white cursor-pointer" @click="back()"><i class="pi pi-angle-left text-3xl"></i></span>
            <ThemeSwitch/>
        </div>
        <div class="flex justify-between px-3 p-1 flex-col bg-white rounded-t-3xl dark:bg-black" 
            :style="{ height: deviceHeight * 0.92 + 'px' }">
          <div class="w-full p-1 mt-8" >
            <p class="font-medium text-slate-800 text-4xl dark:text-gray-400">
                OTP sent
            </p>
            <p class="text-lg leading-6 mt-3 font-normal text-gray-500">
                We have sent an OTP to your mobile number +91 {{ phoneNumber }}
            </p>
            <div class="w-full mt-3">
                <phoneOTP v-model="p_otp"/>

                <div class="w-full mt-1 flex justify-between">
                    <h2 class="font-medium text-lg dark:text-gray-500">00:{{ timeLeft.toString().padStart(2, '0') }}s</h2>

                    <p class="text-xl text-gray-500 font-medium">Resend OTP</p>
                </div>
            </div>
          </div>
          <div class="w-full" >
            <Button
             type="button"
              label="Verify OTP"
               class="primary_color wave-btn text-white w-full py-4 text-xl border-0"
                @click="mobile_signup()"  :disabled="!isOtpValid" >
                {{ buttonText }}
                <span v-if="isAnimating" class="wave"></span>
        </Button>
          </div>
        </div>


    </div>
</template>

<script setup>
import ThemeSwitch from '~/components/darkmode/darkmode.vue'
import phoneOTP from '~/components/forminputs/otpinput.vue'
import { ref, onMounted, watch, watchEffect, onUnmounted } from 'vue';
const deviceHeight = ref(0);
const emit = defineEmits(['updateDiv']);
const timeLeft = ref(60); // Start from 60 seconds
const phoneNumber = ref('')
const isAnimating = ref(false);
const buttonText = ref("Verify OTP");
let timer = null;
const p_otp=ref('')
const props = defineProps({
    data: {
        type: Object,
        default: () => ({}),
    },
});

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

watchEffect(() => {
    const mobileNo = props.data || '';
 
    phoneNumber.value = mobileNo.length >= 10
        ? `${mobileNo.slice(0, 2)}******${mobileNo.slice(-3)}`
        : mobileNo;

   
});

const isOtpValid = computed(() => 
p_otp.value.length === 6
);

const mobile_signup=()=>{
    isAnimating.value = true;
    setTimeout(() => {
      isAnimating.value = false;
      emit('updateDiv', 'div3');
    }, 800); 
}
const back=()=>{
    emit('updateDiv', 'div1');
}
</script>

<style>

</style>