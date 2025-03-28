<template>
    <Toast position="top-left" group="tl" />
    <div class=" relative bg-indigo-100 dark:bg-indigo-900 ">
        <div class="flex justify-end items-center px-3 bg-indigo-100 dark:bg-indigo-900"
            :style="{ height: deviceHeight * 0.08 + 'px' }">
            <ThemeSwitch />
        </div>
        <div class="flex bg-indigo-50 dark:bg-indigo-950 rounded-t-3xl" :style="{ height: deviceHeight * 0.94 + 'px' }">
            <div class="w-1/2 p-2 flex justify-center items-center dk">

            </div>
            <div class="w-1/2 p-2 flex items-center md ">
                <div class="w-full">
                    <p style="font-size: 1.5rem;" class=" text-black dark:text-white p-2">Pan Details</p>
                    <PanInput v-model="panNumber"/>
                    <div class="w-full mt-3">
                        <Button label="Upload PAN" @click="visible = true" severity="info" class="w-full" icon="pi pi-cloud-upload" />
                    </div>

                    <div class="w-full mt-3 p-2" v-if="fileuploadbox">
                        <p style="font-size: 1rem;" class=" text-black dark:text-white p-2">Select PAN Proof</p>
                        <fileinput @file-selected="handleFileUpload" />
                     
                    </div>

                    <div class="w-full mt-3 p-2" v-if="cameracapturebox" >
                        <p style="font-size: 1rem;" class=" text-black dark:text-white p-2">Captured Image</p>
                       <cameramode  v-model="capturedImage"/>
                     
                    </div>
                </div>


            </div>
        </div>

        <div class="flex absolute bg-indigo-100  rounded-t-2xl dark:bg-indigo-900 w-full z-3 bottom-3"
            :style="{ height: deviceHeight * 0.08 + 'px' }">
            <div class="w-full p-1 dk"></div>
            <div class="w-full p-2 py-2 flex justify-center items-center ">
             <Button label="Next" @click="pan_submission()" class="w-full  dark:bg-white border-0"   severity="help" />
            </div>
        </div>

    </div>

    <Dialog v-model:visible="visible" class="p-0" modal header="Upload PAN" :style="{ width: '25rem' }">
        <div class="w-full flex gap-2">
            <div class="w-full p-1 flex flex-col justify-center gap-2 items-center">
                <p><i class="pi pi-upload" style="font-size: 2rem;"></i></p>
                <Button label="File Upload" @click="pan_proof_selectmode('filesupload')" class="w-full" />
            </div>
            <div class="w-full p-1">
                <div class="w-full p-1 flex flex-col justify-center gap-2 items-center">
                    <p><i class="pi pi-camera" style="font-size: 2rem;"></i></p>
                    <Button label="Capture" @click="pan_proof_selectmode('cameramode')" class="w-full" />
                </div>
            </div>
        </div>
    </Dialog>
</template>

<script setup>

import { ref, onMounted } from 'vue';
import PanInput from '~/components/forminputs/paninput.vue'
import ThemeSwitch from '~/components/darkmode/darkmode.vue'
import fileinput from '~/components/pan/panfileinput.vue'
import cameramode from '~/components/pan/cameracapture.vue'

import { useToast } from 'primevue/usetoast';

const toast = useToast();

const visible = ref(false);

const fileuploadbox=ref(false)
const cameracapturebox=ref(false)
const panNumber=ref('')
const capturedImage = ref("");
const deviceHeight = ref(0);
onMounted(() => {
    deviceHeight.value = window.innerHeight;
    window.addEventListener('resize', () => {
        deviceHeight.value = window.innerHeight;

    });
});

const pan_proof_selectmode = (mode) => {
    if (mode === 'filesupload') {
        fileuploadbox.value = true;
        cameracapturebox.value = false; // Close the other box
    } else if (mode === 'cameramode') {
        cameracapturebox.value = true;
        fileuploadbox.value = false; // Close the other box
    }
    visible.value = false;
};

const selectedFiles = ref([]);

const handleFileUpload = (files) => {
    selectedFiles.value = files;
    console.log(selectedFiles.value)
};


const pan_submission=()=>{
    if(!panNumber.value){
        toast.add({ severity: 'error', summary: 'Error Message', detail: 'Pan number is required', group: 'tl', life: 3000 });
    }
    else if (selectedFiles.value.length === 0 && !capturedImage.value) {
        toast.add({ severity: 'error', summary: 'Error Message', detail: 'PAN proof is required (either upload a file or capture an image)', group: 'tl', life: 3000 });
    } 
    else{
        toast.add({ severity: 'success', summary: 'Success', detail: 'PAN submitted successfully', group: 'tl', life: 3000 });
        console.log("PAN Number:", panNumber.value);
        console.log("PAN Number:", panNumber.value);
        console.log("Uploaded Files:", selectedFiles.value);
        console.log("Captured Image:", capturedImage.value);
    }
}

</script>
<style>

</style>