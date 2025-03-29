<template>
    <div class="primary_color">
        <div class="w-full p-2 primary_color" :style="{ height: deviceHeight * 0.40 + 'px' }">
            <div class="w-full px-2 py-2 flex justify-between items-center">
                <Button @click="back()" class="bg-slate-100 border-0 cursor-pointer text-slate-600 py-3 dark:bg-black"><i
                        class="pi pi-angle-left text-xl dark:text-gray-500"></i></Button>
                <ThemeSwitch />
            </div>
            <div class="w-full flex justify-center mt-10 ">
                <span class="text-white" style="font-size: 3rem;">NKYC</span>
            </div>
        </div>

        <div class="w-full p-2   bg-white rounded-t-3xl dark:bg-black"
            :style="{ height: deviceHeight * 0.60 + 'px' }">
            <div class="w-full mt-3 px-3 " >
                <div class="w-full">
                <p class="text-3xl font-bold dark:text-gray-400">Add your email</p>
                <p class="mt-2 leading-6 text-xl font-semibold text-gray-500">This is where we'll send you important updates and insights on the market.</p>
                </div>

                <div class="w-full mt-4">
                    <EmailInput v-model="emailid"/>
                </div>


                <div class="w-full mt-5 ">
                    <Button type="button" label="Continue" class="primary_color text-white w-full py-4 text-xl border-0"   :disabled="!emailid" >
                    </Button>

                    <p class="text-gray-500 text-center mt-1">OR</p>

                    <Button type="button" icon="pi pi-google" label="Continue with Google" class="bg-blue-900 text-white w-full py-4 text-xl border-0 mt-1"   >
                    </Button>
                </div>
               

               

                </div>


          
        </div>
    </div>
</template>

<script setup>

import { ref, onMounted } from 'vue';
import ThemeSwitch from '~/components/darkmode/darkmode.vue'
import EmailInput from '~/components/forminputs/emailinput.vue'

import Button from 'primevue/button';

const emailid = ref('')
const emit = defineEmits(['updateDiv']);

const deviceHeight = ref(0);
onMounted(() => {
    deviceHeight.value = window.innerHeight;
    window.addEventListener('resize', () => {
        deviceHeight.value = window.innerHeight;

    });
});

const back=()=>{
    emit('updateDiv', 'div2');
}


</script>
<style></style>