<template>
    <div class="primary_color" >
        <div class="flex justify-between primary_color items-center px-3"
            :style="{ height: deviceHeight * 0.08 + 'px' }">
            <span @click="back()" class="text-white cursor-pointer"><i class="pi pi-angle-left text-3xl"></i></span>
            <ThemeSwitch />
        </div>
        <div class="flex justify-between flex-col bg-white rounded-t-3xl dark:bg-black"
            :style="{ height: deviceHeight * 0.92 + 'px' }">
            <div class="w-full mt-4 px-5 p-1">
                <p class="text-4xl text-blue-900 font-medium dark:text-gray-400">
                   Cofirm your details
                </p>

                <p class="text-xl mt-2 leading-6 text-gray-500 font-normal">
                    Verify the details fetched from your Aadhaar card.
                </p>
               

                <div class="w-full px-2 py-2 bg-gray-100 rounded-md mt-3 dark:bg-gray-900">
                    <div class="w-full flex gap-3" >
                        <div class="p-1 w-20" >
                            <p class="font-normal text-lg text-gray-500">Name</p>
                        </div>
                        <div class="p-1 " >
                            <p class="font-medium text-xl text-blue-900">G*****m</p>
                        </div>
                    </div>

                    <div class="w-full flex gap-3" >
                        <div class="p-1 w-20" >
                            <p class="font-normal text-lg text-gray-500">Father's<br>Name</p>
                        </div>
                        <div class="p-1 flex justify-evenly gap-10" >
                            <p class="font-medium text-xl text-blue-900">Ra*****n</p>
                            <p class="text-right text-lg text-blue-500">Edit <i class="pi pi-angle-right"></i></p>
                            
                        </div>
                       
                    </div>

                    <div class="w-full flex gap-3" >
                        <div class="p-1 w-20" >
                            <p class="font-normal text-lg text-gray-500">DOB</p>
                        </div>
                        <div class="p-1" >
                            <p class="font-medium text-xl text-blue-900">09*****</p>
                        </div>
                    </div>

                    <div class="w-full flex gap-3" >
                        <div class="p-1 w-20" >
                            <p class="font-normal text-lg text-gray-500">Gender</p>
                        </div>
                        <div class="p-1" >
                            <p class="font-medium text-xl text-blue-900">M*******</p>
                        </div>
                    </div>

                    <div class="w-full flex gap-3" >
                        <div class="p-1 w-20" >
                            <p class="font-normal text-lg text-gray-500">Address</p>
                        </div>
                        <div class="p-1" >
                            <p class="font-medium text-xl text-blue-900">No.64, G*******,<br>N*****, T******</p>
                        </div>
                    </div>
                </div>
                

            </div>

            <div class="w-full p-1 bg-gray-100 rounded-t-3xl dark:bg-gray-900">
                <div class="w-full py-3 flex gap-3 justify-between items-center p-1 mb-1" >
                    <div class="p-2 px-2 flex justify-center items-center static w-14 h-14 bg-blue-600  rounded-full  flex-shrink-0">
                        <span><i class="pi pi-id-card text-2xl text-gray-300"></i></span>
                    </div>
                    <div class="w-full p-1" >
                        <p class="text-xl text-blue-900 font-medium">
                            PAN linked with your Aadhaar Card
                        </p>
                    </div>

                    <span class="text-blue-600 text-lg font-medium flex items-center">view <i class="pi pi-angle-right"></i></span>

                </div>
                <Button type="button"  @click="handleButtonClick"
                    class=" primary_color wave-btn text-white w-full py-4 text-xl border-0  ">
                    {{ buttonText }}
                    <span v-if="isAnimating" class="wave"></span>
                </Button>
            </div>


        </div>

    </div>

   



   
</template>
<script setup>
import ThemeSwitch from '~/components/darkmode/darkmode.vue'
import { ref, onMounted } from 'vue';

const emit = defineEmits(['updateDiv']);
const deviceHeight = ref(0);
const buttonText = ref("Continue");
const isAnimating = ref(false);

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
      emit('updateDiv', 'submission', '1'); 
    }, 800); 
};












</script>
