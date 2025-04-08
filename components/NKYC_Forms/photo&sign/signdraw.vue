<template>
    <div class="primary_color" >
        <div class="flex justify-between primary_color items-center px-3"
            :style="{ height: deviceHeight * 0.08 + 'px' }">
            <span @click="back()" class="text-white cursor-pointer"><i class="pi pi-angle-left text-3xl"></i></span>
            <ThemeSwitch />
        </div>
        <div class="flex justify-between px-3 p-1 flex-col bg-white rounded-t-3xl dark:bg-black"
            :style="{ height: deviceHeight * 0.92 + 'px' }">

            <div class="w-full px-2 mt-4">
                <p class="text-2xl text-blue-900 font-medium dark:text-gray-400">
                   Draw your signature
                </p>
                <p class="text-gray-500 leading-6 font-normal text-md mt-3">
                    Use the signature box to sign
                </p>
                <canvas ref="canvasRef" class="mt-3 border-2 border-dashed rounded-lg"></canvas>
            </div>

            

            <div class="w-full p-1">
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
import { ref, onMounted, onUnmounted } from 'vue';

const deviceHeight = ref(0);
const isAnimating = ref(false);
const buttonText = ref("Continue");
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


onMounted(() => {
    deviceHeight.value = window.innerHeight;
    window.addEventListener('resize', () => {
        deviceHeight.value = window.innerHeight;
    });

    const canvas = canvasRef.value;
  ctx = canvas.getContext('2d');

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

})
const imageSrc = ref('');
const emit = defineEmits(['updateDiv']);
const handleButtonClick=()=>{
    const canvas = canvasRef.value;
  if (!canvas) return;
  imageSrc.value = canvas.toDataURL('image/png'); 
console.log(imageSrc.value)
  isAnimating.value = true;
    setTimeout(() => {
      isAnimating.value = false;
     emit('updateDiv', 'signupload', imageSrc.value);
    }, 800); 

}


const back = () => {
    emit('updateDiv', 'signature');
}
</script>
<style>
canvas {
  display: block;
  width: 100%;
  height: 40vh; /* 30% of viewport height */
  touch-action: none;
  background-color: white;

}
</style>