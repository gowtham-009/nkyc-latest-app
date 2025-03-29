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
    <form4 :data="data" />
  </div>
</template>

<script setup>
import { ref, onMounted, onBeforeMount } from 'vue';
import { useRoute, useRouter } from 'vue-router';
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

const route = useRoute();
const router = useRouter();



onMounted(() => {
if (route.query.dival) {
  currentForm.value = route.query.dival;
  const newQuery = { ...route.query };
  delete newQuery.dival;
  router.replace({ query: newQuery });
}
});


</script>

<style>
</style>
