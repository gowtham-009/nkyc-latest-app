<template>
 
    <div v-if="currentForm === 'div1'">
    <NKYCList @updateDiv="handleUpdateDiv" />
  </div>
  <div v-if="currentForm === 'div2'">
    <PAN_d @updateDiv="handleUpdateDiv" />
  </div>
  <div v-if="currentForm === 'div3'">
    <PAN_1 @updateDiv="handleUpdateDiv" />
  </div>
  
</template>

<script setup>
import NKYCList from '~/components/NKYC_Forms/nkyclist.vue'
import PAN_d from '~/components/NKYC_Forms/pandetails/pan-d.vue'
import PAN_1 from '~/components/NKYC_Forms/pandetails/pan_1.vue'
const currentDiv = ref('');
const currentForm = ref('div1'); // Default form
const handleUpdateDiv = (value) => {

currentDiv.value = value;
currentForm.value=currentDiv.value

};


</script>

<style >
.p-button-text.p-button-secondary{
  display: none !important;
}
</style>