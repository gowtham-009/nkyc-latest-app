<template>
    <div class="card">
        <h1>File Upload</h1>
        <Toast />
        <FileUpload 
            name="demo[]" 
            url="/api/upload" 
            @upload="onAdvancedUpload($event)"  
            accept="image/*,application/pdf" 
            :maxFileSize="1000000" 
            :auto="true"
            :showUploadButton="false"
            :showCancelButton="false"
        >
            <template #empty>
                <span>Drag and drop files here to upload.</span>
            </template>
        </FileUpload>
    </div>
</template>

<script setup>
import { useToast } from "primevue/usetoast";
const toast = useToast();

const onAdvancedUpload = () => {
    toast.add({ severity: 'info', summary: 'Success', detail: 'File Uploaded', life: 3000 });
};
</script>
