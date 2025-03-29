<template>
    <div class="container">
      <Button @click="startAnimation" class="wave-btn">
        {{ buttonText }}
        <span v-if="isAnimating" class="wave"></span>
      </Button>
    </div>
  </template>
  
  <script setup>
  import { ref } from "vue";
  
  const isAnimating = ref(false);
  const buttonText = ref("Click Me");
  
  const startAnimation = () => {
    isAnimating.value = true;
    buttonText.value = "Progress..."; // Change text
  
    setTimeout(() => {
      isAnimating.value = false;
      buttonText.value = "Click Me"; // Reset text after animation
    }, 800); // Match animation duration
  };
  </script>
  
  <style scoped>
  .container {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
  }
  
  .wave-btn {
    position: relative;
    overflow: hidden;
    padding: 12px 24px;
    font-size: 18px;
    background-color: #007bff;
    color: white;
    border: none;
    cursor: pointer;
    border-radius: 8px;
    outline: none;
    transition: background 0.3s ease-in-out;
  }
  
  .wave {
    position: absolute;
    top: 0;
    left: 0;
    width: 0%;
    height: 100%;
    background: rgba(255, 255, 255, 0.3);
    animation: waveMove 0.8s ease-out forwards;
  }
  
  @keyframes waveMove {
    0% {
      width: 0%;
      opacity: 0.6;
    }
    100% {
      width: 100%;
      opacity: 0;
    }
  }
  </style>
  