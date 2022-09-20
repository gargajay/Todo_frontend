<template>
    <ul class="text-right p-4 pr-4 font-semibold bg-gray-100">
        
        <li class="inline mx-2 text-indigo-600 hover:text-pink-400 cursor-pointer" ><router-link to="/">Home</router-link></li>

        
        <li v-if="!isLoggedIn" class="inline mx-2 text-indigo-600 hover:text-pink-400 cursor-pointer" ><router-link to="/login">Login</router-link></li>
        <li v-if="!isLoggedIn" class="inline mx-2 text-indigo-600 hover:text-pink-400 cursor-pointer" ><router-link to="/register">Signup</router-link></li>
        <li v-if="isLoggedIn" class="inline mx-2 text-indigo-600 hover:text-pink-400 cursor-pointer" > <button @click="logout()">Logout</button> </li>

 

    </ul>
   
  </template>
  
  <script>
  export default {
   name: 'appNavbar',
   props: ['isLoggedIn'],
   methods:{
    logout(){
        this.$parent.logout()
    }
   }
  }
  </script>
  
  <style>
  </style>