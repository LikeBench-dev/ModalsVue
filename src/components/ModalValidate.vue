<template>
  <modal
          title="Modal with form + Validate"
          @close="sendEmit">
    <div slot="body">
      <form @submit.prevent="onSubmit">
      
<!--        NAME-->
        <div class="form-item" :class="{ errorInput:  $v.name.$error}">
        <label>Name:</label>
          <p class="errorText" v-if="!$v.name.required"> Field is
            required! </p>
          <p class="errorText" v-if="!$v.name.minLength"> Name must
            have at least {{ $v.name.$params.minLength.min }}! </p>
        <input v-model="name" :class="{error: $v.name.$error }"
               @change="$v.name.$touch()">
        </div>
        
<!--        password-->
 
        <div class="form-item" :class="{ errorInput:  $v.password.$error}">
          <label>Password:</label>
          <p class="errorText" v-if="!$v.password.required"> Field is
            required! </p>
          <p class="errorText" v-if="!$v.password.minLength"> password must
            have at least {{ $v.password.$params.minLength.min }}! </p>
          <input v-model="password" :class="{error: $v.password.$error }"
                 @change="$v.password.$touch()"  type="password">
        </div>
<!--        repeat-->
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
        
        
<!--        EMAIL-->
        <div class="form-item" :class="{ errorInput:  $v.email.$error}">
          <label>Email:</label>
          <p class="errorText" v-if="!$v.email.required"> Field is
            required! </p>
          <p class="errorText" v-if="!$v.email.email"> Email is not
            correct!</p>
          <input v-model="email" :class="{error: $v.email.$error }"
                 @change="$v.email.$touch()">
        </div>
     
<!--                button-->
        <button class="btn btnPrimary" >Submit!</button>
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
            name: '',
            email: '',
            password: '',
            repeatPassword: ''
        }
    },
    validations: {
        name: {
            required,
            minLength: minLength(4)
        },
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
        onSubmit () {
            this.$v.$touch()
            if (!this.$v.$invalid) {
                const user = {
                    name: this.name,
                    email: this.email,
                    password: this.password,
                }
                console.log(user)
                this.name = ''
                this.email = ''
                this.password = ''
                this.repeatPassword = ''
                this.$v.$reset()
                this.$emit('close')
            }
        },
        sendEmit () {
            this.name = ''
            this.email = ''
            this.password = ''
            this.repeatPassword = ''
            this.$v.$reset();
            this.$emit("close");
        }
    }

}
</script>

<style lang="scss">
.form-item .errorText {
  display: none;
  margin-bottom: 8px;
  font-size: 13.4px;
  color: rgba(221, 71, 71, 0.82);
}
.form-item {
  &.errorInput .errorText {
    display: block;
  }
}
  input.error {
    border-color: rgba(221, 71, 71, 0.82);
  }

</style>
