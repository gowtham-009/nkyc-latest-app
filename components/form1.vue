<template>
<Toast position="top-left" group="tl" />
    <div class=" relative bg-indigo-100 dark:bg-indigo-900 ">
        <div class="flex justify-end items-center px-3 bg-indigo-100 dark:bg-indigo-900 "   :style="{ height: deviceHeight * 0.08 + 'px' }">
            <ThemeSwitch/>
        </div>
        <div class="flex bg-indigo-50 dark:bg-indigo-950 rounded-t-3xl"  :style="{ height: deviceHeight * 0.94 + 'px' }">
            <div class="w-1/2 p-2 flex justify-center items-center dk" >
                
            </div>
            <div class="w-1/2 p-2 flex items-center md " >
                <div class="w-full p-2" >
                  <p style="font-size: 2rem;" class=" text-black dark:text-white p-2">Sign-Up</p>
                    <div class="flex flex-col gap-1">
                        <mobileinput  v-model="phoneNumber"/>
                    </div>
                    <div class="flex flex-col gap-1 mt-6">
                        <emailinput v-model="emailID"/>
                    </div>
                    <div class="flex flex-col gap-1 mt-2">
                      <div class="flex gap-2">
                        <checkbox class="dark:text-slate-300"  v-model="remchecked"/>
                      </div>
                    
                    </div>
                </div>
            </div>
        </div>

        <div class="flex absolute bg-indigo-100  rounded-t-2xl dark:bg-indigo-900 w-full z-3 bottom-3"  :style="{ height: deviceHeight * 0.08 + 'px' }">
            <div class="w-full p-1 dk" ></div>
            <div class="w-full p-2 py-2 flex justify-center items-center "  >
                <Button label="Submit" class="w-full  dark:bg-white border-0"  @click="formvalidation()" severity="help" />
            </div>
        </div>

    </div>
</template>

<script setup>

import { ref, onMounted } from 'vue';
import mobileinput from '~/components/forminputs/mobileinput.vue';
import emailinput from '~/components/forminputs/emailinput.vue';
import checkbox from '~/components/forminputs/remembercheckbox.vue';
import { createtoken } from '@/composables/globaltoken';
import { useUrl } from '@/composables/useUrl';
import { useToast } from 'primevue/usetoast';
import ThemeSwitch from '~/components/darkmode/darkmode.vue'

const emit = defineEmits(['updateDiv']);
const toast = useToast();
const { val } = useUrl();
const token = ref(null);
const phoneNumber = ref('');
const emailID = ref('');
const remchecked=ref('')

onMounted(async () => {
    token.value = await createtoken();
});


const deviceHeight = ref(0);
onMounted(() => {
    deviceHeight.value = window.innerHeight;
    window.addEventListener('resize', () => {
        deviceHeight.value = window.innerHeight;

    });
});

const formvalidation=()=>{
   if(!phoneNumber.value){
    toast.add({ severity: 'error', summary: 'error Message', detail: 'Phone no is required', group: 'tl', life: 3000 });
   }
   else if(!emailID.value){
    toast.add({ severity: 'error', summary: 'error Message', detail: 'Email ID is required', group: 'tl', life: 3000 });
   }
   else if(!remchecked.value){
    toast.add({ severity: 'error', summary: 'error Message', detail: 'Please click your checkbox', group: 'tl', life: 3000 });
   }
   else{
   
    signup()
   }
}


const signup = async () => {
  const apiUrl = val.value + 'signup.php';
  const formdata = new FormData();
  const email = emailID.value;

  // Email validation using regex
  const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
  if (!emailRegex.test(email)) {
    toast.add({ 
      severity: 'error', 
      summary: 'Invalid Email', 
      detail: 'Please enter a valid email address.', 
      group: 'tl', 
      life: 3000 
    });
    return; // Stop the function if email is invalid
  }

  formdata.append('mobileno', phoneNumber.value);
  formdata.append('emailid', email);
  formdata.append('token', token.value.token);

  if (token.value.token) {
    try {
      const response = await fetch(apiUrl, {
        method: 'POST',
        body: formdata
      });

      if (!response.ok) {
        throw new Error(`HTTP error! Status: ${response.status}`);
      } else {
        const data = await response.json();
        if (data.status === 'ok') {
          toast.add({ 
            severity: 'success', 
            summary: 'Success', 
            detail: data.message, 
            group: 'tl', 
            life: 3000 
          });
          emit('updateDiv', 'div2', data);
        } else {
          toast.add({ 
            severity: 'error', 
            summary: 'Error', 
            detail: data.message, 
            group: 'tl', 
            life: 3000 
          });
        }
      }
    } catch (error) {
      console.error(error);
    }
  }
};

</script>
<style>
   @import url("~/assets/css/form1.css");
</style>
