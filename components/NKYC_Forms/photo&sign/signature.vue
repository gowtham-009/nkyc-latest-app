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
                    Add your signature
                </p>
                <p class="text-gray-500 leading-6 font-normal text-xl mt-3">
                    Upload an image or use the signature box to sign
                </p>

                <div class="w-full mt-3 rounded-lg px-3 py-3 bg-blue-50 dark:bg-slate-900">
                    <h2 class="text-blue-900 text-2xl font-medium mt-3 dark:text-gray-400">Please remember:</h2>

                    <div class="w-full flex items-center  gap-3 mt-2">
                        <div
                            class="p-2 px-2 flex justify-center items-center static w-12 h-12 bg-gray-200 dark:bg-gray-800 rounded-md flex-shrink-0">
                            <span> <span><i class="pi pi-cog text-xl text-blue-600"></i></span></span>
                        </div>
                        <div class="p-2">
                            <p class="text-gray-500 leading-6 font-normal text-lg">
                               Choose the option to upload an image of your signature for accuracy.
                            </p>
                        </div>
                    </div>

                    <div class="w-full flex items-center  gap-3 mt-2">
                        <div
                        class="p-2 px-2 flex justify-center items-center static w-12 h-12 bg-gray-200 dark:bg-gray-800 rounded-md flex-shrink-0">
                            <span><i class="pi pi-clone text-xl text-blue-600"></i></span>
                        </div>
                        <div class="p-2">
                            <p class="text-gray-500 leading-6 font-normal text-lg">
                               This signature will be used to match any future offline transaction.
                            </p>
                        </div>
                    </div>
                    <div class="w-full flex items-center gap-3 mt-2">
                        <div
                        class="p-2 px-2 flex justify-center items-center static w-12 h-12 bg-gray-200 dark:bg-gray-800 rounded-md flex-shrink-0">
                        <span><i class="pi pi-upload text-xl text-blue-600"></i></span>
                        </div>
                        <div class="p-2">
                            <p class="text-gray-500 leading-6 font-normal text-lg">
                               signature mismatch will require resubmission as per regulations.
                            </p>
                        </div>
                    </div>

                   
                </div>

                <p class="text-gray-500 mt-2 text-lg font-normal text-left">
                    The uploaded photo size should not be more than 5 MB.
                </p>

            </div>

            <div class="w-full p-1">
                
                <Button type="button" @click="handleButtonClick"  
                    class=" primary_color wave-btn text-white w-full py-4 text-xl border-0  ">
                    {{ buttonText }}
                    <span v-if="isAnimating" class="wave"></span>
                </Button>

                <p @click="openFilePicker" class="text-blue-600 text-xl py-3 mt-1 font-medium text-center">
                    Upload from gallery
                </p>
            </div>

        </div>
        <input type="file" ref="fileInput" @change="handleFileChange" accept="image/*" class="hidden" />

    </div>
</template>
<script setup>
import ThemeSwitch from '~/components/darkmode/darkmode.vue'
import { ref, onMounted } from 'vue';

const deviceHeight = ref(0);
const isAnimating = ref(false);
const buttonText = ref("Open signature-box");

onMounted(() => {
    deviceHeight.value = window.innerHeight;
    window.addEventListener('resize', () => {
        deviceHeight.value = window.innerHeight;
    });
});









const emit = defineEmits(['updateDiv']);
const back = () => {

  //  emit('updateDiv', 'div2');
}

const fileInput = ref(null);
const selectedFile = ref(null);
const imageUrl = ref(null);

const openFilePicker = () => {
    if (fileInput.value) {
        fileInput.value.click();
       
       
    }
};

const handleFileChange = (event) => {
    const file = event.target.files[0]; // Get the selected file
    if (file) {
        selectedFile.value = file;
    
        imageUrl.value = URL.createObjectURL(file);
       if(imageUrl.value){
        emit('updateDiv', 'signupload', imageUrl.value);
       }

    }
};

const handleButtonClick = () => {
 isAnimating.value = true;
    setTimeout(() => {
      isAnimating.value = false;
      emit('updateDiv', 'signdraw');
    }, 800); 
};

</script>
