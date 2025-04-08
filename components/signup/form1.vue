<template>
  <div class="primary_color overflow-hidden h-screen">
    <!-- Box 1 -->
    <div
      class="w-full p-2 primary_color transition-all duration-100"
      :style="{ height: box1Height + 'px' }"
    >
      <div class="w-full px-2 py-2 flex justify-end items-center">
        <!-- Optional header stuff -->
      </div>
      <div class="w-full flex justify-center mt-10">
        <span class="text-white text-5xl">NKYC</span>
      </div>
    </div>

    <!-- Box 2 -->
    <div
      v-show="showBox2"
      class="w-full p-2 bg-white dark:bg-black rounded-t-3xl transition-all duration-100"
      :style="{ height: box2Height + 'px' }"
    >
      <div class="w-full mt-3 px-3 flex flex-col justify-between">
        <!-- Your form / content -->
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const box1Height = ref(0);
const box2Height = ref(0);
const showBox2 = ref(false);

onMounted(() => {
  const fullHeight = window.innerHeight;

  // Initial state: full height to box 1, box 2 hidden
  box1Height.value = fullHeight;
  box2Height.value = 0;
  showBox2.value = false;

  // After 2 seconds: show box 2 and animate heights
  setTimeout(() => {
    showBox2.value = true;
    box1Height.value = fullHeight * 0.3;
    box2Height.value = fullHeight * 0.7;
  }, 2000);

  // Optional: handle resize
  window.addEventListener('resize', () => {
    const updatedHeight = window.innerHeight;
    if (!showBox2.value) {
      box1Height.value = updatedHeight;
      box2Height.value = 0;
    } else {
      box1Height.value = updatedHeight * 0.3;
      box2Height.value = updatedHeight * 0.7;
    }
  });
});
</script>

<style scoped>

</style>
