<template>
    <div class="primary_color" >
        <div class="flex justify-between primary_color items-center px-3"
            :style="{ height: deviceHeight * 0.08 + 'px' }">
            <span @click="back()" class="text-white cursor-pointer"><i class="pi pi-angle-left text-3xl"></i></span>
            <ThemeSwitch />
        </div>
        
        
        <div class="w-full flex flex-col justify-between p-2 bg-white rounded-t-3xl dark:bg-black" 
            :style="{ height: deviceHeight * 0.92 + 'px' }">




            <div class="w-full p-2 mt-4">
                <p class="text-4xl text-blue-900 font-medium dark:text-gray-400">
                   Signature added
                </p>

                <p class="text-lg leading-5 text-gray-500 font-normal mt-2">
                   Use the same signature as on your PAN
                </p>

                <div class="w-full flex justify-center mt-2">
                    <div class="w-full border-2 border-dashed flex justify-center py-3"  >
                        <img v-if="signatureData" :src="signatureData" alt="Preview" class="preview-img h-80"  />
                       
                    </div>
                </div>
                <div class="w-full mt-2">
                    <p class="text-blue-950 font-normal text-2xl text-center dark:text-gray-400">Signature looking different?</p>
                    <p @click="fileUpload()" class="text-center font-medium text-blue-600 mt-3 text-2xl">Upload Photo</p>
                </div>
            </div>
            <div class="w-full" >
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
import { ref, onMounted, onBeforeUnmount } from 'vue';
const emit = defineEmits(['updateDiv']);
const deviceHeight = ref(0);
const isAnimating = ref(false);
const buttonText = ref("Continue");
const signatureData = ref('');
const props = defineProps({
    data: {
        type: String,
        default: () => ({}),
    },
});

signatureData.value=props.data
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
       emit('updateDiv', 'submission','4');
    }, 800); 
};


const fileUpload = () => {
    signatureData.value = ''; // Reset signature data

    // Create an input element for file upload
    const input = document.createElement('input');
    input.type = 'file';
    input.accept = 'image/*'; // Accept only image files

    // Handle file selection
    input.addEventListener('change', (event) => {
        const file = event.target.files[0];
        if (file) {
            const reader = new FileReader();
            reader.onload = () => {
                signatureData.value = reader.result; // Store image as base64
            };
            reader.readAsDataURL(file);
        }
    });

    // Trigger file selection dialog
    input.click();
};



const back = () => {
    emit('updateDiv', 'signature');
};






</script>
