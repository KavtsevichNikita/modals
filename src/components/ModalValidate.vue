<template>
     <!-- Validate modal -->
         <modal title="Validate modal"
         @close="$emit('close')">
        <!-- slot -->
          <div slot="body">

            <form @submit.prevent="onSubmit">

                <!-- name -->
                <div class="form-item" :class=" { errorInput: $v.name.$error } ">
              <label>Name:</label>
              <p class="errorText" v-if="!$v.name.required">Field is required!</p>
              <p class="errorText" v-if="!$v.name.minLength">Name must have at least {{$v.name.$params.minLength.min}} !</p>
              <input 
              :class="{ error: $v.name.error }"
              @change="$v.name.$touch()"
              v-model="name">
                </div>


                <!-- email -->
               <div class="form-item" :class=" { errorInput: $v.email.$error } ">
              <label>Email:</label>
              <p class="errorText" v-if="!$v.email.required">Field is required!</p>
              <p class="errorText" v-if="!$v.email.email">Email incorrect!</p>
              <input 
              :class="{ error: $v.email.error }"
              @change="$v.email.$touch()"
              v-model="email">
                </div>


                 <!-- Password -->
               <div class="form-item" :class=" { errorInput: $v.password.$error } ">
              <label>Password:</label>
              <p class="errorText" v-if="!$v.password.required">Field is required!</p>
              <p class="errorText" v-if="!$v.password.minLength">Password must have at least 8!</p>
              <input type="password"
              :class="{ error: $v.password.error }"
              @change="$v.password.$touch()"
              v-model="password">
                </div>



                 <!-- Password Check -->
               <div class="form-item" :class=" { errorInput: $v.repeatPassword.$error } ">
              <label>Password Check:</label>
              <p class="errorText" v-if="!$v.repeatPassword.required">Field is required!</p>
              <p class="errorText" v-if="!$v.repeatPassword.sameAs">Passwords must be identical!</p>
              <input type="password"
              :class="{ error: $v.repeatPassword.error }"
              @change="$v.repeatPassword.$touch()"
              v-model="repeatPassword">
                </div>


                <!-- button -->
              <button class="btn btnPrimary">Submit</button>
            </form>

            <!-- <p>Text Text Text Text Text</p> -->
          </div>
         </modal>
</template>

<script>
import { required, minLength, email, sameAs } from 'vuelidate/lib/validators'
import modal from  "@/components/UI/Modal.vue"

export default {
    components : {modal},
    data () {
        return  {
            email : '',
            name : '',
            password: '',
            repeatPassword: ''
        }
    },
    validations : {
            name : {
                required,
                minLength: minLength(4)
            },
            email : {
                required,
                email
            },
            password : {
                required,
                minLength: minLength(6)
            },
            repeatPassword : {
                required,
                sameAsPassword: sameAs('password')
            }
        },
        methods : {
            onSubmit () {
                this.$v.$touch()
                if (!this.$v.$invalid) {
                    const user = {
                        name: this.name,
                        email: this.email,
                        password:this.password
                    }
                    console.log(user)
                    // Done
                    this.name = '',
                    this.email = '',
                    this.password = '',
                    this.repeatPassword = '',
                    this.$v.$reset()
                    this.$emit('close')
                }
            },
            onClose () {
                this.$v.$reset()
            }
        }
}
</script>

<style lang="scss">

.form-item .errorText {
    display: none;
    margin-bottom: 8px;
    font-size: 13.4px;
    color: red;
}
.form-item {
    &.errorInput .errorText {
    display: block;
} 
}
input.error{
    border-color: red;
}

</style>