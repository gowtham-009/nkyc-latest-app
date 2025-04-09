<template>
    <div class="card w-full">
      <span class="text-lg text-gray-500">Select Relationship</span>
      <AutoComplete class="w-full py-2"  v-model="value" dropdown :suggestions="items" @complete="search"/>
    </div>
  </template>
  
  <script setup>
  import { ref } from "vue";
  
  const value = ref(null);
  const items = ref([]);
  
  const defaultItems = ['Father', 'Mother', 'Sister', 'Brother', 'Spouse', 'Son', 'Daughter'];
  
  const search = (event) => {
    if (event.query) {
      items.value = Array.from({ length: 10 }, (_, i) => `${event.query}-${i}`);
    } else {
      items.value = defaultItems;
    }
  };
  </script>
  