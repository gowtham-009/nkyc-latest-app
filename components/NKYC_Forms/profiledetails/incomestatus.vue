<template>
    <div class="primary_color">
        <div class="flex justify-between primary_color items-center px-3"
            :style="{ height: deviceHeight * 0.08 + 'px' }"> 
            <span @click="back()" class="text-white cursor-pointer">
                <i class="pi pi-angle-left text-3xl"></i>
            </span>
            <ThemeSwitch />
        </div>
        
        <div class="flex justify-between px-3 p-1 flex-col bg-white rounded-t-3xl dark:bg-black"
            :style="{ height: deviceHeight * 0.92 + 'px' }">
            
            <!-- Marital Status -->
            <div class="w-full mt-4 px-2" v-if="activebox === 'marriedbox'">
                <p class="text-2xl text-blue-900 font-medium dark:text-gray-400">
                    Your annual income 
                </p>
                <p class="text-md mt-3 text-gray-500 font-normal leading-6">
                    These details are required by SEBI to open your Demat account.
                </p>
                
                <div class="grid grid-cols-2 gap-2 mt-3">
                    <button v-for="option in options" :key="option.value"
                        @click="selectMaritalStatus(option.value)"
                        :class="[
                            'px-6 py-2 rounded-lg border-2 text-lg font-normal w-full transition-all',
                            selected === option.value
                                ? 'bg-blue-600 border-blue-600 text-white'
                                : 'bg-gray-200 border-gray-300 text-black'
                        ]">
                        {{ option.label }}
                    </button>
                </div>
            </div>

            
          
        </div>
    </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import ThemeSwitch from '~/components/darkmode/darkmode.vue';
const emit=defineEmits(['updateDiv']);
const deviceHeight = ref(0);
const activebox = ref('marriedbox');

// Marital Status
const selected = ref(""); 
const options = [
    { label: "Below 1 lakh", value: "Below 1 lakh" },
    { label: "1 lakh to 5 lakhs", value: "1 lakh to 5 lakhs" },
    { label: "5 lakhs to 10 lakhs", value: "5 lakhs to 10 lakhs" },
    { label: "10 lakhs to 25 lakhs", value: "10 lakhs to 25 lakhs" },
    { label: "Above 25 lakhs", value: "Above 25 lakhs" },
 
];

const selectMaritalStatus = (value) => {
    selected.value = value;
    emit('updateDiv', 'nominee'); 
   
};
const back = () => {
    emit('updateDiv', 'occupation');
};

//'2'

onMounted(() => {
    deviceHeight.value = window.innerHeight;
    window.addEventListener('resize', () => {
        deviceHeight.value = window.innerHeight;
    });
});
</script>
