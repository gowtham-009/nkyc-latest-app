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

            <!-- Marital Status -->
            <div class="w-full mt-4 px-2">
                <p class="text-2xl text-blue-900 font-medium dark:text-gray-400">
                    Add nominee
                </p>
                <p class="text-md mt-1 text-gray-500 font-normal leading-6">
                    Relationship with nominee
                </p>
                <div class="w-full flex flex-col gap-2 mt-3">
                    <Button @click="visible = true" label="Add Nominee"
                        class="w-full py-3 primary_color text-white"></Button>

                    <p class="text-center text-md text-blue-600 mt-2">Skip now</p>
                </div>
            </div>
            <Dialog class="p-0" v-model:visible="visible" modal :style="{ width: '25rem' }">
                <div class="w-full flex justify-between  items-center p-1 mb-0">
                    <span class="text-2xl text-medium">Add nominee</span>
                    <span><i class="pi pi-times"></i></span>
                </div>
                <Namemode class="mt-2" />
                <Name class="mt-2" />
                <Aadharpan class="mt-2" />

                <Address class="mt-2" />
                <Address2 class="mt-2" />
                <Address3 class="mt-2" />

                <div class="w-full mt-2 flex gap-2">
                    <div class="w-full">
                        <Pincode class="mt-2" />
                    </div>
                    <div class="w-full">
                        <State class="mt-2" />
                    </div>
                </div>
                <City class="mt-2" />

                <div class="w-full mt-2">
                    <Button label="Save" class="primary_color w-full text-white py-2"></Button>

                    <p class="text-center py-2 text-blue-600 font-medium">
                        Add another nominee
                    </p>
                </div>
            </Dialog>


            <div class="w-full">
                <Button @click="handleButtonClick"
                    class="primary_color wave-btn w-full text-white  py-4 text-xl border-0">
                    {{ buttonText }}
                    <span v-if="isAnimating" class="wave"></span>
                </Button>
            </div>



        </div>


    </div>



</template>

<script setup>
import { ref, onMounted } from 'vue';
import ThemeSwitch from '~/components/darkmode/darkmode.vue';
import Namemode from '~/components/nomineeinputs/dropdown.vue';
import Name from '~/components/nomineeinputs/nameinput.vue';

import Aadharpan from '~/components/nomineeinputs/aadharpaninput.vue';
import Address from '~/components/nomineeinputs/address.vue';
import Address2 from '~/components/nomineeinputs/address2.vue';
import Address3 from '~/components/nomineeinputs/address3.vue';
import Pincode from '~/components/nomineeinputs/pincode.vue';
import State from '~/components/nomineeinputs/state.vue'
import City from '~/components/nomineeinputs/city.vue'
const visible = ref(false);
const emit=defineEmits(['updateDiv']);
const deviceHeight = ref(0);
const isAnimating = ref(false);
const buttonText = ref("Continue");


const back = () => {
    emit('updateDiv', 'income');
};



onMounted(() => {
    deviceHeight.value = window.innerHeight;
    window.addEventListener('resize', () => {
        deviceHeight.value = window.innerHeight;
    });
});
</script>
<style>
.p-dialog-header{
    padding: 1% !important;
}
</style>