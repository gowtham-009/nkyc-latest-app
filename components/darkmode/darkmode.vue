<template>
  <div>
    <button @click="toggleDarkMode" class="p-2 bg-gray-300 dark:bg-gray-700 rounded-full flex items-center gap-2">
      <i :class="isDark ? 'pi pi-moon text-white' : 'pi pi-sun'"></i>
    </button>
  </div>
</template>

<script setup>
import { useDarkMode } from '@/composables/useDarkMode';
import 'primeicons/primeicons.css'

const { isDark, toggleDarkMode } = useDarkMode();
</script>

<style>
</style>
