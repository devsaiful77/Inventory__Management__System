<template>
    <div>
        <!-- main part -->
        <div class="authincation h-100">
            <div class="container h-100">
                <div class="row justify-content-center h-100 align-items-center">
                    <div class="col-md-6">
                        <div class="authincation-content">
                            <div class="row no-gutters">
                                <div class="col-xl-12">
                                    <div class="auth-form">
                                        <div class="text-center mb-3">
                                            <a href="index.html"><img src="backend/images/logo-full.png" alt=""></a>
                                        </div>
                                        <h4 class="text-center mb-4">Sign up your account</h4>
                                        <form @submit.prevent="register">
                                            <div class="form-group">
                                                <label class="mb-1"><strong>Username</strong></label>
                                                <input type="text" class="form-control" placeholder="username" v-model="form.name">
                                                <small class="text-danger" v-if="errors.name">{{ errors.name[0] }}</small>
                                            </div>
                                            <div class="form-group">
                                                <label class="mb-1"><strong>Email</strong></label>
                                                <input type="email" class="form-control" placeholder="hello@example.com" v-model="form.email">
                                                <small class="text-danger" v-if="errors.email">{{ errors.email[0] }}</small>
                                            </div>
                                            <div class="form-group">
                                                <label class="mb-1"><strong>Password</strong></label>
                                                <input type="password" class="form-control" value="Password" v-model="form.password">
                                                <small class="text-danger" v-if="errors.password">{{ errors.password[0] }}</small>
                                            </div>
                                            <div class="form-group">
                                                <label class="mb-1"><strong>Confirm Password</strong></label>
                                                <input type="password" class="form-control" value="Password" v-model="form.password_confirmation">
                                            </div>
                                            <div class="text-center mt-4">
                                                <button type="submit" class="btn btn-primary btn-block">Sign up</button>
                                            </div>
                                        </form>
                                        <div class="new-account mt-3">
                                            <p>Already have an account?
                                            <router-link to="/" class="text-primary">Sign in</router-link>
                                            </p>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <!-- main part -->
    </div>
</template>

<script>
import axios from 'axios'
import { Toast } from '../../../../public/js/app'
import User from '../../Helpers/User'
export default{
    // ========== first called created method if this methode has been true then execute another script ==========
    created(){
        if(User.loggedIn()){
            this.$router.push({ name: 'home' })
        }
    },
    /*
        ========== Data Binding ==========
    */
    data(){
        return{
            form:{
                name: null,
                email: null,
                password: null,
                confirm_password: null
            },
            errors:{}
        }
    },
    /*
        =========== Methods api operation ===========
    */
   methods:{
       register(){
           axios.post('/api/auth/signup',this.form)
           .then(res => {
               Toast.fire({
                   icon: 'success',
                   title: 'Sign Up in Successfully'
               })
               this.$router.push({ name: 'home' })
           })
           .catch(error => this.errors = error.response.data.errors)
           .catch(
               Toast.fire({
                   icon: 'warning',
                   title: 'Opps! Register Failed'
               })
           )
       }
   }

}
</script>
