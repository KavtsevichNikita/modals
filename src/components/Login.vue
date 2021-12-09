<template>
    <modal 
    title="Sign in"
    @close="$emit('close')">

    <div slot="body">
        <form @submit.prevent="Login">
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
                 <button class="btn btnPrimary">Submit</button>
              <button class="btn btnDanger" @click="openRegistrationForm">Нет аккаунта?</button>
        </form>
        
    </div>
    </modal>
</template>

<script>
import { required, minLength, email} from 'vuelidate/lib/validators'
import modal from './UI/Modal.vue'
export default ({
    components : {
        modal
    },
    data () {
        return {
            email : '',
            password : '',
        }
    },
    validations : {

            email : {
                required,
                email
            },
            password : {
                required,
                minLength: minLength(6)
            }
        },
        methods : {
            Login () {
                this.$v.$touch()
                if (!this.$v.$invalid) {
                    const user = {
                        email: this.email,
                        password:this.password
                    }
                    console.log(user),
                    this.email = '',
                    this.password = ''
                    this.$v.$reset()
                    this.$emit('close')
                    
            }
        },
        // openRegistrationForm () {
        //     this.$Login.$close()
        // }
    }
})
</script>