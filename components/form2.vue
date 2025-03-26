<template>

    <div class="bg-surface-50 dark:bg-surface-950">
        <div class="flex justify-end items-center px-3 " style="border:2px solid red"  :style="{ height: deviceHeight * 0.10 + 'px' }">
            <ThemeSwitch/>
        </div>
        <div class="flex" style="border: 1px solid red;" :style="{ height: deviceHeight * 0.80 + 'px' }">
            <div class="w-1/2 p-2 flex justify-center items-center dk" style="border: 1px solid red;">
               
            </div>
            <div class="w-1/2 p-2 flex items-center md " style="border: 1px solid red;">
                <div class="w-full p-2" >
                    <div class="flex flex-col gap-1 disabled ">
                        <mobileinput/>
                    </div>
                    <div class="flex flex-col gap-1 mt-2">
                        <phoneotp/>
                        <p class="text-right dark:text-gray-100">Resend</p>
                    </div>
                    <div class="flex flex-col gap-1 mt-2 disabled ">
                        <emailinput/>
                    </div>
                    <div class="flex flex-col gap-1 mt-2">
                        <emailotp/>
                        <p class="text-right dark:text-gray-100">Resend</p>
                    </div>
                    <div class="flex flex-col gap-1 mt-2">
                        <referalcode/>
                    </div>
                </div>
            </div>
        </div> 
        <div class="flex" style="border: 1px solid red;" :style="{ height: deviceHeight * 0.10 + 'px' }">
            <div class="w-full p-1 flex items-center hd " style="border:2px solid black">
            </div>
            <div class="w-full p-1 flex justify-between items-center"  style="border:2px solid black">
                <Button label="Preview" @click="signup_page()" class="dark:bg-white text-black border-0" severity="help" />

                <Button label="Next" class="dark:bg-white text-black border-0" severity="help" />

            </div>
        </div>

    </div>
</template>

<script setup>

import { ref, onMounted } from 'vue';
import mobileinput from '~/components/forminputs/mobileinput.vue';
import emailinput from '~/components/forminputs/emailinput.vue';

import phoneotp from '~/components/forminputs/phoneotp.vue';

import emailotp from '~/components/forminputs/emailotp.vue';

import referalcode from '~/components/forminputs/referalcode.vue';

import ThemeSwitch from '~/components/darkmode/darkmode.vue'

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
