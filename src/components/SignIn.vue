<template>
  <modal
          title="Sign in"
          @close="$emit('close')">
    <!--        EMAIL-->
    <div class="container__body" slot="body">
      <form @submit.prevent="singIn">
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
  
  
        <!--                button-->
        <button class="btn btnPrimary">Sign in</button>
      </form>
  
  
      <a @click="openReg">I don't have account</a>

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
        }
    },
    methods: {
        singIn() {
            this.$v.$touch()
            if (!this.$v.$invalid) {
                const user = {
                    email: this.email,
                    password: this.password,
                }
                console.log(user)
                this.email = ''
                this.password = ''
                this.$v.$reset()
                this.$emit('close')
            }
        },
        openReg() {
            this.email = ''
            this.password = ''
            this.$v.$reset()
            this.$emit('openReg')
        }
    }
}

</script>


<style lang="scss" scoped>
.container__body {
  form {
    border-bottom: 1px solid #dcdfe6;
    padding-bottom: 20px;
    margin-bottom:  5px;
  }
  a {
    cursor: pointer;
    font-size: 14px;
  }
}


</style>
