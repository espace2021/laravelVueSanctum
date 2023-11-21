<template>
    <div class="container"> 
        <nav class="navbar navbar-expand-lg navbar-light bg-light">
            <div class="collapse navbar-collapse">
                <div class="navbar-nav">
                    <router-link to="/" class="nav-item nav-link">Dashboard</router-link>
                    <router-link to="/login" class="nav-item nav-link">Login</router-link>
                    <router-link to="/register" class="nav-item nav-link">Register</router-link>
                    <button @click="logout">Logout</button>
                </div>
            </div>
        </nav>
        <router-view> </router-view>
    </div>
</template>
 
<script setup>
import axios from 'axios';

import { useRouter } from 'vue-router';
const router = useRouter();

const   logout=async()=> { 
     await axios.get('/sanctum/csrf-cookie').then(response => {
                axios.post('/logout')
                      .then((response) => {
                        console.log(response)
                        localStorage.removeItem("user")
                        router.push("/login")
                      })
                      .catch(err => {console.log(err);alert(err) })
                 
           })
        }
</script>
