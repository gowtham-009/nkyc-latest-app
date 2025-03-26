<template>
<Toast position="top-left" group="tl" />
    <div class=" bg-surface-50 dark:bg-surface-950">
        <div class="flex justify-end items-center px-3 " style="border:2px solid red"  :style="{ height: deviceHeight * 0.10 + 'px' }">
            <ThemeSwitch/>
        </div>
        <div class="flex " style="border: 1px solid red;" :style="{ height: deviceHeight * 0.80 + 'px' }">
            <div class="w-1/2 p-2 flex justify-center items-center dk" style="border: 1px solid red;">
                
            </div>
            <div class="w-1/2 p-2 flex items-center md " style="border: 1px solid red;">
                <div class="w-full p-2" >
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

        <div class="flex" style="border: 1px solid red;" :style="{ height: deviceHeight * 0.10 + 'px' }">
            <div class="w-full p-1 dk" style="border: 1px solid red;"></div>
            <div class="w-full p-1 flex justify-center items-center " style="border: 1px solid red;" >
                <Button label="submit" class="w-full  dark:bg-white border-0"  @click="formvalidation()" severity="help" />
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
          emit('updateDiv', 'div2');
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
