<template>
  <div v-if="currentForm === 'div1'">
    <form1 @updateDiv="handleUpdateDiv" />
  </div>
  <div v-if="currentForm === 'div2'">
    <form2  :data="data" @updateDiv="handleUpdateDiv" />
  </div>
  <div v-if="currentForm === 'div3'">
    <form3 :data="data" @updateDiv="handleUpdateDiv" />
  </div>
  <div v-if="currentForm === 'div4'">
    <form4 :data="data" @updateDiv="handleUpdateDiv" />
  </div>
</template>

<script setup>
import { ref } from 'vue';

import form1 from '~/components/signup/form1.vue';
import form2 from '~/components/signup/form2.vue';
import form3 from '~/components/signup/form3.vue';
import form4 from '~/components/signup/form4.vue';
const data = ref({});

const currentDiv = ref('');
const currentForm = ref('div1'); // Default form
const handleUpdateDiv = (value, newData = {}) => {

currentDiv.value = value;
currentForm.value=currentDiv.value
data.value = newData;
};




</script>

<style>
</style>
