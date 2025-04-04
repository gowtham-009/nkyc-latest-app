<script setup>
import { ref, onMounted, onUnmounted } from 'vue';

const canvasRef = ref(null);
let ctx = null;
let isDrawing = false;

// 🖊️ Start drawing
const startDrawing = (event) => {
  isDrawing = true;
  const { x, y } = getMousePos(event);
  ctx.beginPath();
  ctx.moveTo(x, y);
};

// ✏️ Drawing
const draw = (event) => {
  if (!isDrawing) return;
  const { x, y } = getMousePos(event);
  ctx.lineTo(x, y);
  ctx.stroke();
};

// 🛑 Stop drawing
const stopDrawing = () => {
  isDrawing = false;
  ctx.beginPath();
};

// Get Mouse/Tap Position
const getMousePos = (event) => {
  const rect = canvasRef.value.getBoundingClientRect();
  let x, y;

  if (event.touches) {
    x = event.touches[0].clientX - rect.left;
    y = event.touches[0].clientY - rect.top;
  } else {
    x = event.clientX - rect.left;
    y = event.clientY - rect.top;
  }

  return { x, y };
};

// Setup Canvas on Mount
onMounted(() => {
  const canvas = canvasRef.value;
  ctx = canvas.getContext('2d');

  // Set Canvas size (Full width, 30% height)
  canvas.width = window.innerWidth;
  canvas.height = window.innerHeight * 0.3;

  ctx.lineCap = 'round';
  ctx.strokeStyle = 'black'; // Default black color
  ctx.lineWidth = 3; // Default stroke thickness

  // Attach event listeners
  canvas.addEventListener('mousedown', startDrawing);
  canvas.addEventListener('mousemove', draw);
  canvas.addEventListener('mouseup', stopDrawing);
  canvas.addEventListener('mouseleave', stopDrawing);

  // Mobile touch support
  canvas.addEventListener('touchstart', startDrawing);
  canvas.addEventListener('touchmove', draw);
  canvas.addEventListener('touchend', stopDrawing);
});

// Cleanup on Unmount
onUnmounted(() => {
  const canvas = canvasRef.value;
  if (!canvas) return;

  canvas.removeEventListener('mousedown', startDrawing);
  canvas.removeEventListener('mousemove', draw);
  canvas.removeEventListener('mouseup', stopDrawing);
  canvas.removeEventListener('mouseleave', stopDrawing);

  canvas.removeEventListener('touchstart', startDrawing);
  canvas.removeEventListener('touchmove', draw);
  canvas.removeEventListener('touchend', stopDrawing);
});
</script>

<template>
  <canvas ref="canvasRef"></canvas>
</template>

<style scoped>
canvas {
  display: block;
  width: 100%;
  height: 30vh; /* 30% of viewport height */
  touch-action: none;
  background-color: white;
  border: 2px solid black; /* 🔲 Added border */
}
</style>
