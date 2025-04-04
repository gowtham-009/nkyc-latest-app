<template>
    <div class="primary_color">
        <div class="flex justify-end primary_color items-center px-3"
            :style="{ height: deviceHeight * 0.08 + 'px' }">
            <ThemeSwitch />
        </div>
        <div class="flex justify-between px-3 p-1 flex-col bg-white rounded-t-3xl dark:bg-black"
            :style="{ height: deviceHeight * 0.92 + 'px' }">
            <div class="w-full mt-4 px-2">
                <p class="text-4xl text-blue-900 font-medium dark:text-gray-400">
                    Link your bank account
                </p>

                <p class="text-xl mt-3 text-gray-500 font-normal leading-6">
                    Select UPI app or scan the QR code to proceed
                </p>


                <div class="w-full px-2 py-3 mt-4 bg-gray-100 rounded-lg dark:bg-gray-900">
                    <div class="flex flex-col justify-center items-start">
                        <div  @click="bank3"
                            class="p-2 px-2 flex justify-center flex-col items-center  w-20 h-20 rounded-full  flex-shrink-0">
                            <img src="https://img.icons8.com/?size=96&id=OYtBxIlJwMGA&format=png" alt="">
                            <p class="text-gray-500 font-medium text-xl">PhoneP</p>
                        </div>

                    </div>
                </div>


                <Divider align="center" class="mt-3" type="dotted">
                    <b class="text-gray-500">OR</b>
                </Divider>

                <div class="w-full flex  gap-2 mt-2 bg-gray-100 rounded-lg py-2 px-2 dark:bg-gray-900" @click="Bankqr2">
                    <div 
                        class="flex justify-center items-center  w-12 h-12 rounded-full  flex-shrink-0">
                        <span><i class="pi pi-qrcode text-2xl dark:text-gray-400"></i></span>
                    </div>

                    <div class="w-full  " >
                        <p class="text-xl mt-3 text-gray-600 font-medium leading-6">
                            Tap to generate QR code
                        </p>
                    </div>

                    <div 
                        class=" flex justify-center   items-center  ">
                        <span><i class="pi pi-angle-right text-xl dark:text-gray-400"></i></span>
                    </div>
                </div>


            </div>

            <div class="w-full flex justify-center p-1" label="Continue">
                <div class="w-3/4 flex gap-2 rounde-t-3xl bg-gray-50 rounded-lg px-2 py-3 dark:bg-gray-900">
                    <p><i class="pi pi-star-fill text-blue-600"></i></p><p class="text-md leading-6 text-gray-500 font-medium text-left">₹1 will be debited to verify your bank account and refunded within 48 working hours</p>
                </div>
            </div>


        </div>

    </div>






</template>
<script setup>
import ThemeSwitch from '~/components/darkmode/darkmode.vue'
import { ref, onMounted } from 'vue';
const emit = defineEmits(['updateDiv']);
const deviceHeight = ref(0);

onMounted(() => {
    deviceHeight.value = window.innerHeight;
    window.addEventListener('resize', () => {
        deviceHeight.value = window.innerHeight;
    });
});






const Bankqr2=()=>{
    emit('updateDiv', 'bankqr2')
}

const bank3=()=>{
  emit('updateDiv', 'bank3')
}







</script>
