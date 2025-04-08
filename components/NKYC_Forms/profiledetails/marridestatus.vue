<template>
    <div class="primary_color">
        <div class="flex justify-end primary_color items-center px-3"
            :style="{ height: deviceHeight * 0.08 + 'px' }"> 
            <ThemeSwitch />
        </div>
        
        <div class="flex justify-between px-3 p-1 flex-col bg-white rounded-t-3xl dark:bg-black"
            :style="{ height: deviceHeight * 0.92 + 'px' }">
            
            <!-- Marital Status -->
            <div class="w-full mt-4 px-2" v-if="activebox === 'marriedbox'">
                <p class="text-2xl text-blue-900 font-medium dark:text-gray-400">
                    Your marital status
                </p>
                <p class="text-md mt-3 text-gray-500 font-normal leading-6">
                    These details are required by SEBI to open your Demat account.
                </p>
                
                <div class="w-full flex gap-2 mt-3">
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

const deviceHeight = ref(0);
const activebox = ref('marriedbox');
const emit = defineEmits(['updateDiv']);
// Marital Status
const selected = ref(""); 
const options = [
    { label: "Unmarried", value: "unmarried" },
    { label: "Married", value: "married" },
];

const selectMaritalStatus = (value) => {
    selected.value = value;
    emit('updateDiv', 'occupation');
};



onMounted(() => {
    deviceHeight.value = window.innerHeight;
    window.addEventListener('resize', () => {
        deviceHeight.value = window.innerHeight;
    });
});
</script>
