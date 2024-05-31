<script setup>

// TODO after user changed value, remove error text

import { computed, ref } from 'vue';

const email = ref('')
const password = ref('')
const confirm_password = ref('')
const term_conditions = ref(null)
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

const terms_password_has_error = computed(() => {
  return error.value.type == 'term_conditions'
})


const validateEmail = (_email) => {
  return String(_email)
    .toLowerCase()
    .match(
      /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|.(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/
    );
};

const validatePassword = (_password) => {
    if (_password == null || _password.length < 8) return 'Password must be at least 8 characters'

    return ''
}

const signup = () => {
    error.value = ''

    if (!validateEmail(email.value)){
        error.value = {
            type: 'email',
            message: 'Enter valid email'
        }
        return
    }

    const password_invalidation = validatePassword(password.value)    
    if (password_invalidation){
        error.value = {
            type: 'password',
            message: password_invalidation
        }
        return
    }

    if (password.value != confirm_password.value){
        error.value = {
            type: 'confirm_password',
            message: 'Confirm password must be matched to password'
        }
        return
    }

    if (term_conditions.value !== true){
        error.value = {
            type: 'term_conditions',
            message: 'You must accept Terms and Conditions'
        }
        return
    }

    // TODO signup with api and login with api

}
</script>
<template>
   <section class="signup-page">
    <div class="container">
        <a href="#" class="logo">
            <img class="w-8 h-8 mr-2" src="https://flowbite.s3.amazonaws.com/blocks/marketing-ui/logo.svg" alt="logo">
            Flowbite    
        </a>
        <div class="form">
            <div class="p-6 space-y-4 md:space-y-6 sm:p-8">
                <h1 class="form-title">
                    Create an account
                </h1>
                <form class="space-y-4 md:space-y-6" action="#" ref="signup_form">
                    <div>
                        <label for="email" class="block mb-2 text-sm font-medium " :class="{'text-gray-900 dark:text-white':!email_has_error, 'text-red-600': email_has_error}">Your email</label>
                        <input v-model="email" type="email" name="email" id="email" class="email" :class="{'border-gray-300 dark:border-gray-600': !email_has_error, 'border-red-600':  email_has_error}" placeholder="name@company.com" required>
                    </div>
                    <div>
                        <label for="password" class="block mb-2 text-sm font-medium" :class="{'text-gray-900 dark:text-white': !password_has_error, 'text-red-600':password_has_error}">Password</label>
                        <input v-model="password" type="password" name="password" id="password" placeholder="••••••••" class="password" :class="{'border-gray-300 dark:border-gray-600': !password_has_error, 'border-red-600': password_has_error}" required> 
                    </div>
                    <div>
                        <label for="confirm-password" class="block mb-2 text-sm font-medium" :class="{'text-gray-900 dark:text-white': !confrirm_password_has_error, 'text-red-600':confrirm_password_has_error}">Confirm password</label>
                        <input v-model="confirm_password" type="confirm-password" name="confirm-password" id="confirm-password" placeholder="••••••••" class="confirm-password" :class="{'border-gray-300 dark:border-gray-600': !confrirm_password_has_error, 'border-red-600': confrirm_password_has_error}" required>
                    </div>
                    <div class="flex items-start">
                        <div class="flex items-center h-5">
                            <input v-model="term_conditions" id="terms" aria-describedby="terms" type="checkbox" class="terms focus:ring-3" required="">
                        </div>
                        <div class="ml-3 text-sm">
                            <label for="terms" class="font-light"  :class="{'text-gray-900 dark:text-white': !terms_password_has_error, 'text-red-600':terms_password_has_error}">I accept the <a class="font-medium text-primary-600 hover:underline dark:text-primary-500" href="#">Terms and Conditions</a></label>
                        </div>
                    </div>
                    <div class="text-red-600 text-[12px]" style="margin-top: 2px;" v-if="error.type">
                         {{ error.message }}
                    </div>
                    <button type="button" class="submit" @click="signup" >Create an account</button>
                    <p class="text-sm font-light text-gray-500 dark:text-gray-400">
                        Already have an account? <a href="#" class="font-medium text-primary-600 hover:underline dark:text-primary-500">Login here</a>
                    </p>
                </form>
            </div>
        </div>
    </div>
   </section>
</template>

<style>

</style>