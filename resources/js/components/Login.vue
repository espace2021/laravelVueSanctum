<template>
    <div class="container">
        <div class="row justify-content-center">
            <div class="col-md-8">

               
                <div class="card card-default">
                    <div class="card-header">Login</div>
                    <div class="card-body">
                        <form>
                            <div class="form-group row">
                                <label for="email" class="col-sm-4 col-form-label text-md-right">E-Mail Address</label>
                                <div class="col-md-6">
                                    <input id="email" type="email" class="form-control" v-model="user.email" required
                                           autofocus autocomplete="off">
                                </div>
                            </div>

                            <div class="form-group row">
                                <label for="password" class="col-md-4 col-form-label text-md-right">Password</label>
                                <div class="col-md-6">
                                    <input id="password" type="password" class="form-control" v-model="user.password"
                                           required autocomplete="off">
                                </div>
                            </div>

                            <div class="form-group row mb-0">
                                <div class="col-md-8 offset-md-4">
                                    <button type="submit" class="btn btn-primary" @click="handleLogin">
                                        Login
                                    </button>
                                </div>
                            </div>
                        </form>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
  import axios from "axios"
  
  import { useRouter } from 'vue-router';
  const router = useRouter() 

      let  user= {}

    const   handleLogin=async()=> { 
       await axios.get('/sanctum/csrf-cookie').then(response => {
                axios.post('http://localhost:8000/api/auth/login', user)
                      .then(response => (
                        
                         router.push({ name: 'dashboard' })
                      ))
                      .catch(err => {console.log(err);alert(err) })
                 
            })
        }
  </script>
