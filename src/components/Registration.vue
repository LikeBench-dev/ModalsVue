<template>
  <modal
          title="Registration"
          @close="$emit('close')">
    
    <!--        EMAIL-->
    <div class="container__body" slot="body">
      <form @submit.prevent="reg">
        <div class="form-item" :class="{ errorInput:  $v.email.$error}">
          <label>Email:</label>
          <p class="errorText" v-if="!$v.email.required"> Field is
            required! </p>
          <p class="errorText" v-if="!$v.email.email"> Email is not
            correct!</p>
          <input v-model="email" :class="{error: $v.email.$error }"
                 @change="$v.email.$touch()">
        </div>
  
  
        <!--password-->
  
        <div class="form-item" :class="{ errorInput:  $v.password.$error}">
          <label>Password:</label>
          <p class="errorText" v-if="!$v.password.required"> Field is
            required! </p>
          <p class="errorText" v-if="!$v.password.minLength"> password must
            have at least {{ $v.password.$params.minLength.min }}! </p>
          <input v-model="password" :class="{error: $v.password.$error }"
                 @change="$v.password.$touch()"  type="password">
        </div>
  
        <!--password repeat-->
        <div class="form-item" :class="{ errorInput:  $v.repeatPassword.$error}">
          <label>repeat Password:</label>
          <p class="errorText" v-if="!$v.repeatPassword"> Field is
            required! </p>
          <p class="errorText"
             v-if="!$v.repeatPassword.sameAsPassword">Passwords must be
            identical.</p>
    
          <input v-model="repeatPassword" :class="{error: $v.repeatPassword.$error }"
                 @change="$v.repeatPassword.$touch()"  type="password">
        </div>
        <!--                button-->
        <button class="btn btnPrimary">Registration</button>
      </form>
      
    </div>
  </modal>


</template>

<script>
import { required, minLength, email, sameAs } from 'vuelidate/lib/validators'

import modal from '@/components/UI/Modal.vue'

export default {
    components: {
        modal
    },
    data () {
        return {
            email: '',
            password: '',
            repeatPassword: ''
        }
    },
    validations: {
        email: {
            required,
            email
        },
        password: {
            required,
            minLength: minLength(6)
        },
        repeatPassword: {
            sameAsPassword: sameAs('password')
        }
    },
    methods: {
        reg() {
            this.$v.$touch()
            if (!this.$v.$invalid) {
                const user = {
                    email: this.email,
                    password: this.password,
                }
                console.log(user)
                this.email = ''
                this.password = ''
                this.repeatPassword = ''
                this.$v.$reset()
                this.$emit('close')
            }
        }
    }
}

</script>


<style lang="scss">


</style>
