<script setup>
import { ref, onMounted, onUnmounted } from "vue";
const props = defineProps(['modelValue']);
const emit = defineEmits(['update:modelValue']);



const videoRef = ref(null);
const canvasRef = ref(null);
const photo = ref(null);
const isCaptured = ref(false);
const stream = ref(null);
const isFrontCamera = ref(true);

const startCamera = async () => {
  try {
    const constraints = {
      video: { facingMode: isFrontCamera.value ? "user" : "environment" }
    };
    stream.value = await navigator.mediaDevices.getUserMedia(constraints);
    if (videoRef.value) {
      videoRef.value.srcObject = stream.value;
      videoRef.value.style.height = `${window.innerHeight * 0.4}px`;
      videoRef.value.style.width = `${(window.innerHeight * 0.4) * (4 / 3)}px`;
    }
  } catch (error) {
    console.error("Error accessing camera:", error);
  }
};

const stopCamera = () => {
  if (stream.value) {
    stream.value.getTracks().forEach(track => track.stop());
    stream.value = null;
  }
};

const capturePhoto = () => {
  if (!videoRef.value || !canvasRef.value) return;
  const ctx = canvasRef.value.getContext("2d");
  canvasRef.value.height = window.innerHeight * 0.4;
  canvasRef.value.width = canvasRef.value.height * (4 / 3); // Maintain aspect ratio
  ctx.drawImage(videoRef.value, 0, 0, canvasRef.value.width, canvasRef.value.height);
  photo.value = canvasRef.value.toDataURL("image/png"); // Convert to base64
  isCaptured.value = true;
  emit("update:modelValue", photo.value);
  stopCamera();
};

const retakePhoto = () => {
  photo.value = null;
  isCaptured.value = false;
  startCamera();
};

const toggleCamera = () => {
  stopCamera();
  isFrontCamera.value = !isFrontCamera.value;
  startCamera();
};

onMounted(() => {
  startCamera();
});

onUnmounted(() => {
  stopCamera();
});
</script>

<template>
  <div class="camera-container">
    <video v-if="!isCaptured" ref="videoRef" autoplay></video>
    <canvas ref="canvasRef" style="display: none"></canvas>
    <img v-if="photo" :src="photo" alt="Captured Image" class="captured-image" />
    <div class="button-container">
      <Button @click="isCaptured ? retakePhoto() : capturePhoto()"><i class="pi pi-camera"></i>
        {{ isCaptured ? "Retake" : "Capture" }}
      </Button>
      <Button @click="toggleCamera"><i class="pi pi-arrow-right-arrow-left"></i>Flip</Button>
    </div>
  </div>
</template>

<style scoped>
.camera-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 10px;
}
video, .captured-image {

  border-radius: 15px;
}
.button-container {
  display: flex;
  gap: 10px;
}
button {
  padding: 10px;
  background: #007bff;
  color: white;
  border: none;
  cursor: pointer;
  border-radius: 5px;
}
</style>