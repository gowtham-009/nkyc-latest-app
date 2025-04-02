<template>
    <div class="primary_color">
        <div class="flex justify-between primary_color items-center px-3"
            :style="{ height: deviceHeight * 0.08 + 'px' }">
            <span @click="back()" class="text-white cursor-pointer"><i class="pi pi-angle-left text-3xl"></i></span>
            <ThemeSwitch />
        </div>
        <div class="flex justify-between px-3 p-1 flex-col bg-white rounded-t-3xl dark:bg-black" v-if="contbox"
            :style="{ height: deviceHeight * 0.92 + 'px' }">
            <div class="w-full mt-4 px-2" v-if="contbox">

                <Card class="dark:bg-gray-900">

                    <template #content>
                        <div class="w-full flex justify-between">
                            <img src="https://img1.digitallocker.gov.in/digilocker-landing-page/assets/img/DigilockerLogo.svg"
                                alt="">
                            <img src="https://cdn-icons-png.flaticon.com/128/17096/17096051.png" width="50" height="50"
                                alt="">
                        </div>
                    </template>
                </Card>

                <Card class="mt-3 ">

                    <template #content>
                        <div class="w-full">
                            <p class="text-black text-xl leading-7 font-medium dark:text-gray-400">
                                Please provide your consent to share the following with <span class="font-bold">Ventura
                                    Securities Onboarding:</span>
                            </p>
                        </div>

                        <Accordion value="0">
                            <AccordionPanel value="0">
                                <AccordionHeader class="text-lg ">Issued Documents(3)</AccordionHeader>
                                <AccordionContent>
                                    <div class="flex py-3 items-center justify-between gap-2">
                                        <label for="ingredient4"><i class="pi pi-id-card text-xl"></i> Aadhaar Card
                                            (XX7817) </label>
                                        <Checkbox v-model="val1" inputId="ingredient4" name="val1" />

                                    </div>
                                    <hr>
                                    <div class="flex py-3 items-center justify-between gap-2">
                                        <label for="ingredient4"><i class="pi pi-verified text-xl"></i> Driving
                                            License(can be accessed) </label>
                                        <Checkbox inputId="ingredient4" name="val1" />

                                    </div>
                                    <hr>
                                    <div class="flex py-3 items-center justify-between gap-2">
                                        <label for="ingredient4"><i class="pi pi-lock text-xl"></i> Digilocker Drive
                                        </label>
                                        <Checkbox inputId="ingredient4" name="val1" />
                                    </div>
                                    <hr>
                                    <div class="flex py-3 items-center justify-between gap-2">
                                        <label for="ingredient4"><i class="pi pi-user text-xl"></i> Profile Information
                                        </label>
                                        <!-- <Checkbox v-model="val1" inputId="ingredient4" name="val1"  /> -->

                                    </div>
                                    <hr>
                                    <div class="flex py-3 items-center justify-between gap-2">
                                        <label for="ingredient4"><i class="pi pi-envelope text-xl"></i> Get your Email
                                        </label>
                                        <!-- <Checkbox v-model="val1" inputId="ingredient4" name="val1"  /> -->

                                    </div>
                                    <hr>
                                    <div class="flex py-3 items-center justify-between gap-2">
                                        <label for="ingredient4"><i class="pi pi-ban text-xl"></i> Not available
                                        </label>
                                        <!-- <Checkbox v-model="val1" inputId="ingredient4" name="val1"  /> -->

                                    </div>
                                </AccordionContent>
                            </AccordionPanel>
                        </Accordion>
                    </template>
                </Card>



            </div>




        </div>

        <div class="flex justify-center items-center px-3 p-1 flex-col bg-white rounded-t-3xl dark:bg-black" v-if="loading"
            :style="{ height: deviceHeight * 0.92 + 'px' }">

            <div class="card flex justify-center">
                <ProgressSpinner />
            </div>
        </div>

    </div>


    <Drawer v-model:visible="visibleBottom" position="bottom" style="height: auto">
        <p class="text-black text-lg leading-6 dark:text-gray-400">
            Consent validity is subject to applicable laws.
        </p>

        <p class="text-black text-lg leading-6 mt-2 dark:text-gray-400">
            By clicking 'Allow', you are giving consent to share with <span class="font-bold">Ventura Securities
                Onboarding</span>.
        </p>

        <div class="w-full mt-3">
            <Button label="Deny" class="w-full text-blue-600 bg-white" />

            <Button label="Allow" @click="allow()" class="w-full text-white bg-blue-600 mt-3" />
        </div>
    </Drawer>



</template>
<script setup>
import ThemeSwitch from '~/components/darkmode/darkmode.vue'
import { ref, onMounted, onBeforeUnmount } from 'vue';

const deviceHeight = ref(0);
const val1 = ref(false)
const visibleBottom = ref(true)
const contbox = ref(true)
const loading = ref(false)
onMounted(() => {
    deviceHeight.value = window.innerHeight;
    window.addEventListener('resize', () => {
        deviceHeight.value = window.innerHeight;
    });
});




const emit = defineEmits(['updateDiv']);

const allow = () => {
    visibleBottom.value = false
    contbox.value = false

    loading.value = true

    setTimeout(() => {
        loading.value = false
        emit('updateDiv', 'div9');
    }, 2000)
}








</script>
