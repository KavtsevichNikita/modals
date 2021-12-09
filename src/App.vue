<template>
  <div class="wrapper">

    <!-- <header></header> -->

    <div class="wrapper-content">
      <section>
        <div class="container">
          
          

          <!-- first modal -->
          <button class="btn btnPrimary" @click="modalFirst = !modalFirst">Show first modal</button>
         <modals title="First modal"
         v-show="modalFirst"
         @close="modalFirst= false">
         <!-- slot -->
          <div slot="body">

            <p>Text Text Text Text Text</p>

            <button class="btn btnPrimary" style="margin-top:10px;" @click="modalFirst = !modalFirst">Well Done!</button>
          </div>
         </modals>




          <!-- second modal -->

          <button class="btn btnPrimary" @click="modalSecond.show = !modalSecond.show">Show second modal</button>
         <modals title="Second modal"
         v-show="modalSecond.show"
         @close="modalSecond.show= false">
         <!-- slot -->
          <div slot="body">

            <form @submit.prevent="submitSecondForm">
              <label>Name:</label>
              <input type="text" required v-model="modalSecond.name">
              <label>Email:</label>
              <input type="email" required v-model="modalSecond.email">
              <button class="btn btnPrimary">Submit</button>
            </form>

            <!-- <p>Text Text Text Text Text</p> -->
          </div>
         </modals>

        <!-- modal with Validate -->
        <button class="btn btnPrimary" @click="modalValidate = !modalValidate">Show Validate Form</button>
        <modalValidate @close="modalValidate = false" v-show="modalValidate"/>
        
        <!-- Login modal -->
        <button class="btn btnPrimary"  @click="login = !login">Sign in</button>
        <login  @close="login = false" v-show="login"/>

        <!-- Registration modal -->
        <button class="btn btnPrimary"  @click="registrationModal = !registrationModal">Registration</button>
        <registration  @close="registrationModal = false" v-show="registrationModal"/>
        


         
        </div>
      </section>
    </div>

    <!-- <footer></footer> -->

  </div>
</template>

<script>
import modals from "@/components/UI/Modal.vue"
import modalValidate  from "@/components/ModalValidate.vue"
import registration from './components/Registration.vue'
import login from './components/Login.vue'
export default {
  components : {
    modals, modalValidate,registration, login
  },
  data () {
    return {
      modalFirst : false,
      modalSecond : {
        show : false,
        name : '',
        email : '',
      },
      modalValidate : false,
      registrationModal : false,
      login : false
      
    }
  },
  methods : {
    submitSecondForm () {
      console.log({
        name: this.modalSecond.name,
        email: this.modalSecond.email
      })
      this.modalSecond.name = '',
      this.modalSecond.email = '',
      this.modalSecond.show = false
    }
  }
}
</script>

<style>
</style>
