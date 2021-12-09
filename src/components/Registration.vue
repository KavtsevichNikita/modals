<template>
    <modal 
    title="Registration form" 
    @close="$emit('close')">
        <div slot="body">
            <form @submit.prevent="Registration">
                <div class="form-item" :class=" { errorInput: $v.login.$error } ">
              <label>Login:</label>
              <p class="errorText" v-if="!$v.login.required">Field is required!</p>
              <p class="errorText" v-if="!$v.login.minLength">Login must have at least {{$v.login.$params.minLength.min}} !</p>
              <input 
              :class="{ error: $v.login.error }"
              @change="$v.login.$touch()"
              v-model="login">
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
              <button class="btn btnDanger">Уже есть аккаунт?</button>
            </form>
        </div>
    </modal>
</template>

<script>
import { required, minLength, email, sameAs } from 'vuelidate/lib/validators'
import modal from  "@/components/UI/Modal.vue"

export default ({
    components : {
        modal
    },
    data () {
        return {
            login : '',
            email : '',
            password : '',
            repeatPassword : '',
        }
    },
    validations : {
            login : {
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
            Registration () {
                this.$v.$touch()
                if (!this.$v.$invalid) {
                    const newUser = {
                        login: this.login,
                        email: this.email,
                        password:this.password
                    }
                    console.log(newUser)
                    // Done
                    this.login = '',
                    this.email = '',
                    this.password = '',
                    this.repeatPassword = '',
                    this.$v.$reset()
                    this.$emit('close')
                }
            }
        }
})
</script>


<style lang="scss" scoped>
.btnDanger{
    margin-left: 40px;
}
</style>