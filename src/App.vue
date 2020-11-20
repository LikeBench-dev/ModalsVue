<template>

  <div class="wrapper">
  
    
    <div class="wrapper-content">
      <section>
        <div class="container">
  
          <!--first modal-->
          <button class="btn btnPrimary" @click="modalFirst = !modalFirst">Show First Modal</button>
          <modals
                  title="First modal"
                  v-show="modalFirst"
                  @close="modalFirst = false">
            <div slot="body">
              <p>TextTextTextTextText</p>
              <button class="btn btnPrimary" @click="modalFirst =
              !modalFirst">Well Done!</button>
            </div>
          </modals>
  
  
          <!--Second modal-->
          <button class="btn btnPrimary"
                  @click="modalSecond.show = !modalSecond.show">Show
            Second Form
            Modal</button>
          <modals
                  title="Modal with form"
                  v-show="modalSecond.show"
                  @close="modalSecond.show = false">
            <div slot="body">
              <form @submit.prevent="SubmitSecondForm">
                <label>Name:</label>
                <input type="text" required v-model="modalSecond.name">
                <label>Email:</label>
                <input type="email" v-model="modalSecond.email">
                <button class="btn btnPrimary" >Submit!</button>
              </form>
              
            </div>
          </modals>
          
<!--          modal with Validate-->
          <button class="btn btnPrimary" @click="modalValidate = !modalValidate">
            Show modal with form + validate</button>
          <modalValidate v-show="modalValidate" @close="modalValidate =
          false"/>

          <div class="homeWork" >
            <!--          SING IN modal-->
            <button class="btn btnPrimary" @click="signIn = !signIn">
              Sign In</button>
            <signIn v-show="signIn" @close="signIn =
          false" @openReg="openReg"/>
  
  
            <!--          registration modal-->
            <button class="btn btnPrimary" @click="registration = !registration">
              Registration</button>
            <registration v-show="registration" @close="registration =
          false"/>
          </div>
          

        </div>
      </section>
    </div>
  </div>
</template>

<script>
import modals from '@/components/UI/Modal.vue'
import modalValidate from '@/components/ModalValidate.vue'
import signIn from '@/components/SignIn.vue'
import registration from '@/components/Registration.vue'
export default {
    components: {
        modals, modalValidate, signIn, registration
    },
    data () {
        return {
            modalFirst: false,
            modalSecond: {
                show: false,
                name: '',
                email: ''
            },
            modalValidate: false,
            signIn: false,
            registration: false
        }
    },
    methods: {
        SubmitSecondForm() {
            console.log({
                name: this.modalSecond.name,
                email: this.modalSecond.email
            })
            this.modalSecond.name = ''
            this.modalSecond.email = ''
            this.modalSecond.show = false
        },
        openReg () {
            this.signIn = false
            this.registration = true
        }
    }
}
</script>

<style lang="scss" scoped>

.container {
  .homeWork {
    width: 50%;
    display: flex;
    flex-flow: wrap;
    justify-content: space-around;
  }
  display: flex;
  flex-flow: wrap;
  justify-content: space-around;
  button {
    margin: 3em 0;
  }
}
</style>
