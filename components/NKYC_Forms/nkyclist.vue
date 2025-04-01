<template>
    <div>
        <div class="w-full dark:bg-black" :class="{ 'primary_color_list': isPrimaryColor }">
            <div class="w-full p-2 "  :style="{ height: deviceHeight * 0.15 + 'px' }">
                <div class="w-full flex justify-end">
                    <ThemeSwitch @click="togglePrimaryColor" />
                </div>
                <div class="w-full flex justify-center mt-2">
                    <!-- something -->
                </div>
            </div>
            <div class="w-full p-2 flex flex-col justify-between" 
                :style="{ height: deviceHeight * 0.85 + 'px' }">
                <div class="w-full p-1" >
                    <div class="w-full">
                        <p class="text-4xl text-center text-blue-600 font-bold">
                            Here's what's next
                        </p>
                    </div>


                    <div class="w-full px-4 mt-2">
                        <div class="w-full flex gap-5">
                            <div class="w-14 h-14 md:w-16 md:h-16 sm:w-20 sm:h-20 bg-blue-200 dark:bg-slate-900  rounded-full flex justify-center items-center p-2">
                                <span><i class="pi pi-folder-open text-blue-900 text-3xl md:text-4xl"></i></span>
                            </div>
                            <div class=" p-1">
                                <p class="text-xl font-bold text-blue-950 dark:text-gray-400">Complete e-KYC</p>
                                <p class="text-md font-semibold text-gray-500">Keep your Aadhaar and PAN card handy</p>
                            </div>
                        </div>

                        <div class="w-full flex gap-5 mt-2">
                            <div class="w-14 h-14 md:w-16 md:h-16 sm:w-20 sm:h-20 bg-blue-200 dark:bg-slate-900  rounded-full flex justify-center items-center p-1">
                                <span><i class="pi pi-user text-blue-900 text-3xl" ></i></span>
                            </div>
                            <div class="p-1">
                                <p class="text-xl font-bold text-blue-950 dark:text-gray-400">Set up your profile</p>
                                <p class="text-md font-semibold text-gray-500">Answer a few question about yourself</p>
                            </div>
                        </div>

                        <div class="w-full flex gap-5 mt-2">
                            <div class="w-14 h-14 md:w-16 md:h-16 sm:w-20 sm:h-20 bg-blue-200 dark:bg-slate-900 rounded-full flex justify-center items-center p-1">
                                <span><i class="pi pi-credit-card text-blue-900 text-3xl" ></i></span>
                            </div>
                            <div class="p-1">
                                <p class="text-xl font-bold text-blue-950 dark:text-gray-400">Link your bank a/c</p>
                                <p class="text-md font-semibold text-gray-500">Set the primary account for your
                                    transactions</p>
                            </div>
                        </div>

                        <div class="w-full flex gap-5 mt-2">
                            <div class="w-14 h-14 md:w-16 md:h-16 sm:w-20 sm:h-20 bg-blue-200 dark:bg-slate-900 rounded-full flex justify-center items-center p-1">
                                <span><i class="pi pi-verified text-blue-900 text-3xl" ></i></span>
                            </div>
                            <div class="p-1">
                                <p class="text-xl font-bold text-blue-950 dark:text-gray-400">Confirm it's you</p>
                                <p class="text-md font-semibold text-gray-500">Click a photo and submit your signature
                                </p>
                            </div>
                        </div>

                        <div class="w-full flex gap-5 mt-2">
                            <div class="w-14 h-14 md:w-16 md:h-16 sm:w-20 sm:h-20 bg-blue-200 dark:bg-slate-900 rounded-full flex justify-center items-center p-1">
                                <span><i class="pi pi-pen-to-square text-blue-900 text-3xl"></i></span>
                            </div>
                            <div class="p-1">
                                <p class="text-xl font-bold text-blue-950 dark:text-gray-400">eSign and Login</p>
                                <p class="text-md font-semibold text-gray-500">Sign your application and start investing
                                </p>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="w-full">
                    <Button type="button" label="Continue" @click="handleButtonClick"
                        class=" primary_color wave-btn text-white w-full py-4 text-xl border-0  ">
                        {{ buttonText }}
                        <span v-if="isAnimating" class="wave"></span>
                    </Button>
                </div>

            </div>

        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue';
import ThemeSwitch from '~/components/darkmode/darkmode.vue';
const emit = defineEmits(['updateDiv']);
const isPrimaryColor = ref(true);
const buttonText = ref("Continue");
const isAnimating = ref(false);
const togglePrimaryColor = () => {
    isPrimaryColor.value = !isPrimaryColor.value;
};

const deviceHeight = ref(0);
onMounted(() => {
    deviceHeight.value = window.innerHeight;
    window.addEventListener('resize', () => {
        deviceHeight.value = window.innerHeight;
    });
});



const handleButtonClick = () => {
 isAnimating.value = true;
    setTimeout(() => {
      isAnimating.value = false;
      emit('updateDiv', 'div2');
    }, 800); 
};

</script>
