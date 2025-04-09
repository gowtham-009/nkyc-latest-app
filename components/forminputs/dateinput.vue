<template>
    <label for="dob">DOB</label>
  <div class="relative w-full">
  
    <input
      ref="datepicker"
      type="text"
      class="bd outline-none bg-gray-50 p-2 py-3 pr-10 rounded-lg w-full"
      placeholder="As per PAN - DD/MM/YYYY"
    />
    <!-- Icon positioned absolutely inside the input -->
    <span class="absolute right-3 top-1/2 -translate-y-1/2 text-gray-500 pointer-events-none">
      📅
    </span>
  </div>
</template>

<script setup>
import { onMounted, ref, defineEmits  } from 'vue'
import flatpickr from 'flatpickr'
import 'flatpickr/dist/flatpickr.min.css'

const datepicker = ref(null)
const emit = defineEmits(['update:dob']) // define emitted event

onMounted(() => {
  flatpickr(datepicker.value, {
    dateFormat: 'd-m-Y',
    allowInput: false, // Prevent typing
    onChange: function(selectedDates, dateStr) {
      emit('update:dob', dateStr) // emit selected date to parent
    }
  })
})
</script>

<style>
  .bd{
    border: 1px solid rgb(173, 173, 173);
  }
</style>