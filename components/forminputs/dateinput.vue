
<template>
          <label for="" class="text-gray-600 text-lg font-semibold">DOB</label>
    <div class="card flex justify-center">
        <DatePicker placeholder="As per PAN - DD/MM/YYYY" v-model="date" class="w-full" showIcon  dateFormat="dd/mm/yy" />
    </div>
</template>

<script setup>
import { ref, watch } from "vue";

const props = defineProps(['modelValue']);
const emit = defineEmits(['update:modelValue']);

const date = ref(props.modelValue || '');

// Watch for changes to the date and emit the updated value to the parent
watch(date, (newValue) => {
  emit('update:modelValue', newValue);
});
</script>
