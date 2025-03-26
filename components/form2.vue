<template>

    <div class="relative bg-indigo-100 dark:bg-indigo-900">
        <div class="flex justify-end items-center px-3 bg-indigo-100 dark:bg-indigo-900  ":style="{ height: deviceHeight * 0.06 + 'px' }">
            <ThemeSwitch/>
        </div>
        <div class="flex bg-indigo-50  rounded-t-3xl dark:bg-indigo-950" :style="{ height: deviceHeight * 0.94 + 'px' }">
            <div class="w-1/2 p-2 flex justify-center items-center dk" >
               
            </div>
            <div class="w-1/2 p-2 flex items-center md ">
                <div class="w-full p-2" >
                   
                    <div class="flex flex-col gap-1 mt-2">
                       <div class="w-full flex">
                            <div class="w-full p-2" >
                                <p class="text-gray-500 text-right dark:text-white" style="font-size: 1.5rem;">Mobile OTP</p>
                            </div>
                            <div class="w-full p-2" >
                                <phoneotp/>
                            </div>
                       </div>
                        <div class="w-full flex justify-between items-center">
                            <span class="dark:text-white">{{ phoneNumber }}</span>
                            <Button label="Resend" severity="secondary" rounded />
                        </div>
                    </div>
                   
                  
                    <div class="flex flex-col mt-2">
                        <div class="w-full flex">
                            <div class="w-full p-2" >
                                <p class="text-gray-500 text-right dark:text-white" style="font-size: 1.5rem;">Email OTP</p>
                            </div>
                            <div class="w-full p-2" >
                                <emailotp/>
                            </div>

                       </div>
                       <div class="w-full flex justify-between items-center">
                            <span class="dark:text-white">{{ emailID }}</span>
                            <Button label="Resend" severity="secondary" rounded />
                        </div>
                    </div>
                  
                    <div class="flex flex-col gap-1 mt-2">
                        <referalcode/>
                    </div>
                </div>
            </div>
        </div> 
        <div class="flex absolute bg-indigo-100  rounded-t-3xl dark:bg-indigo-900 w-full z-3 bottom-1" :style="{ height: deviceHeight * 0.08 + 'px' }">
            <div class="w-full p-1 flex items-center hd " >
            </div>
            <div class="w-full p-1 px-2 flex justify-between items-center gap-2"  >
                <Button label="Preview" @click="signup_page()" class="w-full dark:bg-white  border-0" severity="help" />
                <Button label="Next" @click="otpverfication()" class="w-full dark:bg-white  border-0" severity="help" />
            </div>
        </div>

    </div>
</template>

<script setup>

import { ref, onMounted, watchEffect  } from 'vue';

import phoneotp from '~/components/forminputs/phoneotp.vue';
import emailotp from '~/components/forminputs/emailotp.vue';
import referalcode from '~/components/forminputs/referalcode.vue';
import ThemeSwitch from '~/components/darkmode/darkmode.vue'

const props = defineProps({
  data: {
    type: Object,
    default: () => ({}),
  },
});

const phoneNumber = ref('')
const emailID =ref('')



const p_otp=ref('')
const e_otp=ref('')
const deviceHeight = ref(0);



onMounted(() => {
    deviceHeight.value = window.innerHeight;
    window.addEventListener('resize', () => {
        deviceHeight.value = window.innerHeight;
    });
  
   
});

const emit = defineEmits(['updateDiv']);
const signup_page=()=>{
    emit('updateDiv', 'div1');
}

watchEffect(() => {
    const mobileNo = props.data.mobile_no || '';
  phoneNumber.value = mobileNo.length >= 10 
    ? `${mobileNo.slice(0, 2)}******${mobileNo.slice(-3)}` 
    : mobileNo;

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

const otpverfication=()=>{
    console.log("ph:", p_otp.value)
    console.log('em:', e_otp.value)
    alert('successfully verified')
}
</script>
<style>

.disabled {
  pointer-events: none;
  opacity: 0.5;
}

@media(max-width:992px){
    .hd{
        display:none !important;
    }
   
}
</style>
