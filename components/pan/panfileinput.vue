<template>
    <div class="card">
        <Toast />
        <FileUpload 
            name="demo[]" 
            accept="image/*,application/pdf" 
            :maxFileSize="1000000" 
            :auto="true"
            :showUploadButton="false"
            :showCancelButton="false"
            @select="onFileSelect"
        >
        
            <template #empty>
                <span>Drag and drop files here to upload.</span>
            </template>
        </FileUpload>
    </div>
</template>

<script setup>
import { defineEmits, onMounted } from "vue";

const emit = defineEmits(["file-selected"]);

const onFileSelect = (event) => {
    emit("file-selected", event.files); // Emit files to parent
};

onMounted(() => {
    document.addEventListener("click", (event) => {
        if (event.target.classList.contains("p-fileupload-file-thumbnail")) {
            alert("Image clicked: " + event.target.src);
        }
    });
});
</script>
