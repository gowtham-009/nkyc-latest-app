<template>
    <div>
        <div class="w-full flex flex-col justify-between p-2 h-screen dark:bg-black"
            :class="{ 'primary_color_list': isPrimaryColor }">
            <div class="w-full p-2" >
                <div class="w-full flex justify-end p-1">
                    <ThemeSwitch @click="togglePrimaryColor" />
                </div>
                <div class="w-full flex justify-center">
                    <span class="text-black mt-2" style="font-size: 3rem;">NKYC</span>
                </div>

                <div class="w-full">
                    <p class="text-4xl text-center text-blue-600 font-bold">
                        Here's what's next
                    </p>
                </div>

                <div class="w-full px-4 mt-2" >
                    <div class="w-full flex gap-5">
                        <div class="w-16 h-16 bg-blue-200  rounded-full flex justify-center items-center p-1">
                            <span><i class="pi pi-folder-open text-blue-900" style="font-size: 1.5rem;"></i></span>
                        </div>
                        <div class=" p-1" >
                            <p class="text-xl font-bold text-blue-950">Complete e-KYC</p>
                            <p class="text-md font-semibold text-gray-500">Keep your Aadhaar and PAN card handy</p>
                        </div>
                    </div>

                    <div class="w-full flex gap-5 mt-2">
                        <div class="w-16 h-16 bg-blue-200  rounded-full flex justify-center items-center p-1">
                            <span><i class="pi pi-user text-blue-900" style="font-size: 1.5rem;"></i></span>
                        </div>
                        <div class="p-1">
                            <p class="text-xl font-bold text-blue-950">Set up your profile</p>
                            <p class="text-md font-semibold text-gray-500">Answer a few question about yourself</p>
                        </div>
                    </div>

                    <div class="w-full flex gap-5 mt-2">
                        <div class="w-16 h-16 bg-blue-200  rounded-full flex justify-center items-center p-1">
                            <span><i class="pi pi-credit-card text-blue-900" style="font-size: 1.5rem;"></i></span>
                        </div>
                        <div class="p-1" >
                            <p class="text-xl font-bold text-blue-950">Link your bank a/c</p>
                            <p class="text-md font-semibold text-gray-500">Set the primary account for your transactions</p>
                        </div>
                    </div>

                    <div class="w-full flex gap-5 mt-2">
                        <div class="w-16 h-16 bg-blue-200  rounded-full flex justify-center items-center p-1">
                            <span><i class="pi pi-verified text-blue-900" style="font-size: 1.5rem;"></i></span>
                        </div>
                        <div class="p-1" >
                            <p class="text-xl font-bold text-blue-950">Confirm it's you</p>
                            <p class="text-md font-semibold text-gray-500">Click a photo and submit your signature</p>
                        </div>
                    </div>

                    <div class="w-full flex gap-5 mt-2">
                        <div class="w-16 h-16 bg-blue-200  rounded-full flex justify-center items-center p-1">
                            <span><i class="pi pi-pen-to-square text-blue-900" style="font-size: 1.5rem;"></i></span>
                        </div>
                        <div class="p-1" >
                            <p class="text-xl font-bold text-blue-950">eSign and Login</p>
                            <p class="text-md font-semibold text-gray-500">Sign your application and start investing</p>
                        </div>
                    </div>
                </div>
            </div>
            <div class="w-full">
                <Button type="button" label="Continue" 
            class=" primary_color text-white w-full py-4 text-xl border-0  "
            @click="handleButtonClick">
           
          </Button>
            </div>

        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue';
import ThemeSwitch from '~/components/darkmode/darkmode.vue';

const isPrimaryColor = ref(true);

const togglePrimaryColor = () => {
    isPrimaryColor.value = !isPrimaryColor.value;
};
</script>
