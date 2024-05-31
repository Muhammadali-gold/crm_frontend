<script setup>


import { computed, ref } from 'vue';

const email = ref('')
const password = ref('')
const confirm_password = ref('')
const error = ref({
    type: "",
    message: ""
})

const email_has_error = computed(() => {
  return error.value.type == 'email'
})

const password_has_error = computed(() => {
  return error.value.type == 'password'
})

const confrirm_password_has_error = computed(() => {
  return error.value.type == 'confirm_password'
})

const mode = ref('SEND_INSTRUCTIONS') // SEND_INSTRUCTIONS, PASSWORD_RESETTING, ERROR_TOKEN

if (q('token') != null){

    mode.value = 'SEND_INSTRUCTIONS'
}

const resetPassword = ()=>{

}

</script>

<template>
    <section class="signup-page">
        <div class="container">
            <a href="#" class="logo">
                <img class="w-8 h-8 mr-2" src="https://flowbite.s3.amazonaws.com/blocks/marketing-ui/logo.svg" alt="logo">
                Flowbite    
            </a>
            <div  v-if="mode != 'ERROR_TOKEN'" class="form">
                <div class="p-6 space-y-4 md:space-y-6 sm:p-8">
                    <h1 class="form-title">
                        Reset password
                    </h1>
                    <form class="space-y-4 md:space-y-6" action="#" ref="signup_form">
                        <div v-if="mode == 'SEND_INSTRUCTIONS'">
                            <label for="email" class="block mb-2 text-sm font-medium " :class="{'text-gray-900 dark:text-white':!email_has_error, 'text-red-600': email_has_error}">Your email</label>
                            <input v-model="email" type="email" name="email" id="email" class="email" :class="{'border-gray-300 dark:border-gray-600': !email_has_error, 'border-red-600':  email_has_error}" placeholder="name@company.com" required>
                        </div>
                        <div v-if="mode == 'PASSWORD_RESETTING'">
                            <label for="password" class="block mb-2 text-sm font-medium" :class="{'text-gray-900 dark:text-white': !password_has_error, 'text-red-600':password_has_error}">Password</label>
                            <input v-model="password" type="password" name="password" id="password" placeholder="••••••••" class="password" :class="{'border-gray-300 dark:border-gray-600': !password_has_error, 'border-red-600': password_has_error}" required> 
                        </div>
                        <div v-if="mode == 'PASSWORD_RESETTING'">
                            <label for="confirm-password" class="block mb-2 text-sm font-medium" :class="{'text-gray-900 dark:text-white': !confrirm_password_has_error, 'text-red-600':confrirm_password_has_error}">Confirm password</label>
                            <input v-model="confirm_password" type="confirm-password" name="confirm-password" id="confirm-password" placeholder="••••••••" class="confirm-password" :class="{'border-gray-300 dark:border-gray-600': !confrirm_password_has_error, 'border-red-600': confrirm_password_has_error}" required>
                        </div>
                        <!-- <div class="flex items-start">
                            <div class="flex items-center h-5">
                                <input v-model="term_conditions" id="terms" aria-describedby="terms" type="checkbox" class="terms focus:ring-3" required="">
                            </div>
                            <div class="ml-3 text-sm">
                                <label for="terms" class="font-light"  :class="{'text-gray-900 dark:text-white': !terms_password_has_error, 'text-red-600':terms_password_has_error}">I accept the <a class="font-medium text-primary-600 hover:underline dark:text-primary-500" href="#">Terms and Conditions</a></label>
                            </div>
                        </div> -->
                        <div class="text-red-600 text-[12px]" style="margin-top: 2px;" v-if="error.type">
                            {{ error.message }}
                        </div>
                        <button type="button" class="submit" @click="resetPassword" >Save</button>
                        <!-- <p class="text-sm font-light text-gray-500 dark:text-gray-400">
                            Already have an account? <a href="#" class="font-medium text-primary-600 hover:underline dark:text-primary-500">Login here</a>
                        </p> -->
                    </form>
                </div>
            </div>

            <div v-else>
                Token xato
            </div>
        </div>
   </section>
</template>


<style>

</style>