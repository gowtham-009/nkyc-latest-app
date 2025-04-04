<template>
   <div class="flex flex-col justify-center items-center">
      <div class="camera-wrapper" :class="{ captured: imageCaptured }">
        <video ref="video" autoplay playsinline class="camera-video" v-if="!imageCaptured && cameraActive" />
        <img v-if="imageCaptured" :src="capturedImage" alt="Captured Face" class="camera-image" />
        <canvas ref="canvas" class="hidden"></canvas>
      </div>
  
      <span class="mt-4 dark:text-gray-400">Face distance score: {{ Math.min(faceDistanceScore, 100).toFixed(2) }}</span>
      <span class="dark:text-gray-400">Face Visible: {{ faceProperlyVisible ? '✅ Yes' : '❌ No' }}</span>
</div>
  </template>
  
  <script setup>
  import { ref, onMounted, defineEmits } from 'vue'
  import * as faceapi from 'face-api.js'
  const emit = defineEmits(['imageCaptured']) // Define emit event


  // State refs
  const video = ref(null)
  const canvas = ref(null)
  const capturedImage = ref(null)
  const imageCaptured = ref(false)
  const cameraActive = ref(true)
  const faceDistanceScore = ref(0)
  const faceProperlyVisible = ref(false)
  
  let mediaStream = null
  let closedFrames = 0
  let alertTriggered = false
  const CLOSED_FRAMES_THRESHOLD = 15
  
  // Load Face API models
  const loadModels = async () => {
    await faceapi.nets.tinyFaceDetector.loadFromUri('/models/tiny_face_detector')
    await faceapi.nets.faceLandmark68Net.loadFromUri('/models/face_landmark_68')
  }
  
  // Calculate distance between two points
  const distance = (p1, p2) => Math.hypot(p1.x - p2.x, p1.y - p2.y)
  
  // Calculate Eye Aspect Ratio (EAR) for blink detection
  const calculateEAR = (eye) => {
    const vertical1 = distance(eye[1], eye[5])
    const vertical2 = distance(eye[2], eye[4])
    const horizontal = distance(eye[0], eye[3])
    return (vertical1 + vertical2) / (2.0 * horizontal)
  }
  
  // Detect if eyes are closed
  const areEyesClosed = (leftEye, rightEye) => {
    const threshold = 0.2
    return calculateEAR(leftEye) < threshold && calculateEAR(rightEye) < threshold
  }
  
  // Detect faces and validate conditions
  const detectFaces = async () => {
    if (!video.value || video.value.readyState !== 4 || imageCaptured.value) return
  
    const detections = await faceapi
      .detectAllFaces(video.value, new faceapi.TinyFaceDetectorOptions())
      .withFaceLandmarks()
  
    // 🚨 If no face is detected
    if (detections.length === 0) {
      faceProperlyVisible.value = false
      closedFrames = 0
      alertTriggered = false
      return
    }
  
    // 🚨 If multiple faces are detected
    if (detections.length > 1) {
      alert("Multiple faces detected. Please position only one face in the frame.");
      faceProperlyVisible.value = false;
      return;
    }
  
    const landmarks = detections[0].landmarks
    const leftEye = landmarks.getLeftEye()
    const rightEye = landmarks.getRightEye()
  
    // Get eye center points
    const getCenter = (eye) => {
      const sum = eye.reduce((acc, pt) => ({ x: acc.x + pt.x, y: acc.y + pt.y }), { x: 0, y: 0 })
      return { x: sum.x / eye.length, y: sum.y / eye.length }
    }
    const leftCenter = getCenter(leftEye)
    const rightCenter = getCenter(rightEye)
  
    // Calculate face distance score
    faceDistanceScore.value = distance(leftCenter, rightCenter)
  
    // Check if eyes are closed
    if (areEyesClosed(leftEye, rightEye)) {
      closedFrames++
      if (closedFrames >= CLOSED_FRAMES_THRESHOLD && !alertTriggered) {
        alert('Eyes are closed too long!')
        alertTriggered = true
      }
      return
    } else {
      closedFrames = 0
      alertTriggered = false
    }
  
    // ✅ Check if the face is fully visible
    if (detections[0].detection.score < 0.9) {
      faceProperlyVisible.value = false
      
      return
    } else {
      faceProperlyVisible.value = true
    }
  
    // ✅ Capture image only if face distance > 95 and face is fully visible
    if (faceDistanceScore.value >= 85 && !imageCaptured.value && faceProperlyVisible.value) {
      captureImage()
    }
  }
  
  // Capture image
  const captureImage = () => {
    const ctx = canvas.value.getContext('2d')
    canvas.value.width = video.value.videoWidth
    canvas.value.height = video.value.videoHeight
    ctx.drawImage(video.value, 0, 0, canvas.value.width, canvas.value.height)
    capturedImage.value = canvas.value.toDataURL('image/png')
    imageCaptured.value = true
    emit('imageCaptured', capturedImage.value)
    stopCamera()
  }
  
  // Stop camera after capture
  const stopCamera = () => {
    if (mediaStream) {
      mediaStream.getTracks().forEach((track) => track.stop())
      cameraActive.value = false
    }
  }
  
  // Start face detection loop
  const startDetectionLoop = () => {
    const loop = async () => {
      await detectFaces()
      requestAnimationFrame(loop)
    }
    loop()
  }
  
  // Initialize camera
  onMounted(async () => {
    await loadModels()
    try {
      mediaStream = await navigator.mediaDevices.getUserMedia({ video: true })
      if (video.value) {
        video.value.srcObject = mediaStream
        video.value.onloadeddata = () => {
          startDetectionLoop()
        }
      }
    } catch (err) {
      console.error('Camera error:', err)
    }
  })
  </script>
  
  <style scoped>
  .camera-wrapper {
    width: 300px;
    height: 300px;
    border-radius: 50%;
    overflow: hidden;
    border: 4px solid #00BFFF;
    box-shadow: 0 0 15px rgba(0, 191, 255, 0.5);
    transition: border-color 0.3s ease, box-shadow 0.3s ease;
  }
  
  .camera-wrapper.captured {
    border-color: #00FF00;
    box-shadow: 0 0 20px rgba(0, 255, 0, 0.6);
  }
  
  .camera-video,
  .camera-image {
    width: 100%;
    height: 100%;
    object-fit: cover;
    border-radius: 50%;
  }
  
  canvas.hidden {
    display: none;
  }
  </style>
  