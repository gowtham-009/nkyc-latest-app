<template>
 
    <div v-if="currentForm === 'div1'">
    <NKYCList @updateDiv="handleUpdateDiv" />
  </div>
  <div v-if="currentForm === 'div2'">
    <PAN_1/>
  </div>
  
</template>

<script setup>
import NKYCList from '~/components/NKYC_Forms/nkyclist.vue'
import PAN_1 from '~/components/NKYC_Forms/pandetails/pan_1.vue'
const currentDiv = ref('');
const currentForm = ref('div1'); // Default form
const handleUpdateDiv = (value) => {

currentDiv.value = value;
currentForm.value=currentDiv.value

};


</script>

<style >

</style>