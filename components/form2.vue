<template>

    <div class="bg-surface-50 dark:bg-surface-950">
        <div class="flex justify-end items-center px-3 "   :style="{ height: deviceHeight * 0.08 + 'px' }">
            <ThemeSwitch/>
        </div>
        <div class="flex" :style="{ height: deviceHeight * 0.86 + 'px' }">
            <div class="w-1/2 p-2 flex justify-center items-center dk" >
               
            </div>
            <div class="w-1/2 p-2 flex items-center md ">
                <div class="w-full p-2" >
                    <div class="flex flex-col gap-1 disabled ">
                        <mobileinput  v-model="phoneNumber"/>
                    </div>
                    <div class="flex flex-col gap-1 mt-2">
                        <phoneotp v-model="p_otp"/>
                        <p class="text-right dark:text-gray-100">Resend</p>
                    </div>
                    <div class="flex flex-col gap-1 mt-2 disabled ">
                        <emailinput v-model="emailID"/>
                    </div>
                  

                    <div class="flex flex-col gap-1 mt-2">
                        <emailotp v-model="e_otp"/>
                        <p class="text-right dark:text-gray-100">Resend</p>
                    </div>
                    <div class="flex flex-col gap-1 mt-2">
                        <referalcode/>
                    </div>
                </div>
            </div>
        </div> 
        <div class="flex" :style="{ height: deviceHeight * 0.06 + 'px' }">
            <div class="w-full p-1 flex items-center hd " >
            </div>
            <div class="w-full p-1 flex justify-between items-center gap-2"  >
                <Button label="Preview" @click="signup_page()" class="sz dark:bg-white  border-0" severity="help" />
                <Button label="Next" @click="otpverfication()" class="sz dark:bg-white  border-0" severity="help" />
            </div>
        </div>

    </div>
</template>

<script setup>

import { ref, onMounted, watchEffect  } from 'vue';
import mobileinput from '~/components/forminputs/mobileinput.vue';
import emailinput from '~/components/forminputs/emailinput.vue';
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
  
    phoneNumber.value= props.data.mobile_no
    emailID.value=props.data.email_id
});

const emit = defineEmits(['updateDiv']);
const signup_page=()=>{
    emit('updateDiv', 'div1');
}

watchEffect(() => {
  phoneNumber.value = props.data.mobile_no || '';
  emailID.value = props.data.email_id || '';
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
    .sz{
        width: 100% !important;
    }
}
</style>
