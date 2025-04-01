<template>
    <div class="primary_color">
        <div class="flex justify-between primary_color items-center px-3"
            :style="{ height: deviceHeight * 0.08 + 'px' }">
            <span class="text-white cursor-pointer" @click="back()"><i class="pi pi-angle-left text-3xl"></i></span>
            <ThemeSwitch />
        </div>
        <div class="flex justify-between px-3 p-1 flex-col bg-white rounded-t-3xl dark:bg-black"
            :style="{ height: deviceHeight * 0.92 + 'px' }">
            <div class="w-full mt-4 px-2">
                <p class="text-4xl text-blue-900 font-bold">
                    Upload Pan card
                </p>
                <p class="text-gray-500 leading-6 font-bold text-lg">
                    Click a photo of your PAN card or upload from files
                </p>

                <div class="w-full mt-3 rounded-lg px-3 py-3 bg-blue-50 dark:bg-slate-900">
                    <h2 class="text-blue-900 font-bold mt-3">Please remember:</h2>
                    <div class="w-full flex gap-3 mt-3" >
                        <div class="p-2 bg-blue-200 flex justify-center items-center rounded-lg" >
                            <span><i  class="text-4xl text-blue-900 pi pi-id-card"></i></span>
                        </div>
                        <div class="p-2" >
                            <p class="text-gray-500 font-bold text-lg">
                                Upload only the front-side of your PAN card.
                            </p>
                        </div>
                    </div>
                    <div class="w-full flex gap-3 mt-2">
                        <div class="p-2 bg-blue-200  flex justify-center items-center rounded-lg" >
                            <span><i  class="text-4xl text-blue-900 pi pi-image"></i></span>
                        </div>
                        <div class="p-2" >
                            <p class="text-gray-500 font-bold text-lg">
                                Photo size must not exceed 5MB each.
                            </p>
                        </div>
                    </div>
                    <div class="w-full flex gap-3 mt-2" >
                        <div class="p-2 bg-blue-200  flex justify-center items-center rounded-lg">
                            <span><i  class="text-4xl text-blue-900 pi pi-star"></i></span>
                        </div>
                        <div class="p-2" >
                            <p class="text-gray-500 font-bold text-lg">
                              Photo must be well-lit and glare-free.
                            </p>
                        </div>
                    </div>
                    <div class="w-full flex gap-3 mt-2">
                        <div class="p-2 bg-blue-200  flex justify-center items-center rounded-lg" >
                            <span><i  class="text-4xl text-blue-900 pi pi-image"></i></span>
                        </div>
                        <div class="p-2" >
                            <p class="text-gray-500 font-bold text-lg">
                              Photo must be Clear.
                            </p>
                        </div>
                    </div>
                </div>

            </div>

            <div class="w-full p-1" label="Continue">
                <Button type="button" label="Continue" @click="handleButtonClick"
                        class=" primary_color wave-btn text-white w-full py-4 text-xl border-0  ">
                    </Button>
            </div>

        </div>


    </div>
</template>

<script setup>
import ThemeSwitch from '~/components/darkmode/darkmode.vue'

import { ref, onMounted } from 'vue';
const deviceHeight = ref(0);

onMounted(() => {
    deviceHeight.value = window.innerHeight;
    window.addEventListener('resize', () => {
        deviceHeight.value = window.innerHeight;
    });





});

const back = () => {
    emit('updateDiv', 'div1');
}
</script>

<style></style>