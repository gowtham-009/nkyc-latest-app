<template>
    <div class="primary_color">
        <div class="flex justify-between primary_color items-center px-3"
            :style="{ height: deviceHeight * 0.08 + 'px' }">
            <span @click="back()" class="text-white cursor-pointer"><i class="pi pi-angle-left text-3xl"></i></span>
            <ThemeSwitch />
        </div>
        <div class="flex justify-between px-3 p-1 flex-col bg-white rounded-t-3xl dark:bg-black"
            :style="{ height: deviceHeight * 0.92 + 'px' }">
            <div class="w-full mt-4 px-2">
                <p class="text-4xl  text-blue-950 font-bold dark:text-gray-400">
                    Enter your PAN detail
                </p>
                <p class="text-gray-500 leading-5 font-bold text-xl mt-3">These details are required by SEBI to open
                    your Demat account.</p>

                <div class="w-full mt-4">
                    <paninput v-model="panno" />
                </div>

                <div class="w-full mt-4">
                    <DOB v-model="dateval"/>
                </div>

                <Divider align="center" type="dotted" class="mt-4">
                    <b class="text-gray-600">OR</b>
                </Divider>

                <p class=" text-center text-xl font-bold text-blue-600" @click="panphoto">Upload your PAN Card</p>

                <div class="w-full mt-3">
                    <Pancheck v-model="checkboxval"/>
                </div>
                <div class="w-full flex gap-3 px-2 py-2 mt-4 bg-gray-100 rounded-lg dark:bg-gray-900">
                   <p><i class="pi pi-star-fill text-xl text-yellow-400"></i></p>
                    <p class=" text-gray-500 ">Your account would be opened as per your PAN card details. Plese use the <span class="font-semibold">Offline Account Opening Form</span> if you are looking to open an HUF, Corporate, Partnership, Joint or NRI account.</p>
                </div>
            </div>

            <div class="w-full p-1" label="Continue">
                <Button type="button"  :disabled="!panno || !dateval || !checkboxval"   @click="handleButtonClick"
                    class=" primary_color wave-btn text-white w-full py-4 text-xl border-0  ">
                    {{ buttonText }}
                    <span v-if="isAnimating" class="wave"></span>
                </Button>
            </div>

        </div>
    </div>




</template>
<script setup>
import ThemeSwitch from '~/components/darkmode/darkmode.vue'
import { ref, onMounted } from 'vue';
import paninput from '~/components/forminputs/paninput.vue';
import DOB from '~/components/forminputs/dateinput.vue'
import Pancheck from '~/components/forminputs/pancheck.vue'
const deviceHeight = ref(0);
const isAnimating = ref(false);
const buttonText = ref("Continue");
const panno=ref('')
const dateval=ref('')
const checkboxval=ref('')

onMounted(() => {
    deviceHeight.value = window.innerHeight;
    window.addEventListener('resize', () => {
        deviceHeight.value = window.innerHeight;
    });
});
const emit = defineEmits(['updateDiv']);
const back = () => {

    emit('updateDiv', 'div1');
}

const panphoto=()=>{
    emit('updateDiv', 'div3');
}

const handleButtonClick = () => {
 isAnimating.value = true;
    setTimeout(() => {
      isAnimating.value = false;
     
    }, 800); 
};
</script>
