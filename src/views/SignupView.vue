<template>
    <div class="container w-full max-w-md space-y-8 mx-auto my-20 px-6 py-6 shadow">
   
   <h1 class="text-indigo-600 font-bold font-sans text-4xl text-center">Register</h1>
   <div class="h-0.5 bg-gray-200 w-36 mx-auto mt-2.5"></div>
   <form class="mt-8 space-y-6" action="#" method="POST">
       <div class="-space-y-px rounded-md shadow-sm">
        <div>
           <label for="email-address" class="sr-only">Name</label>
           <input id="email-address" v-model="name" name="name" type="text" autocomplete="name" required class="relative block w-full appearance-none rounded-none rounded-t-md border border-gray-300 px-3 py-2 text-gray-900 placeholder-gray-500 focus:z-10 focus:border-indigo-500 focus:outline-none focus:ring-indigo-500 sm:text-sm" placeholder="Name">
         </div>
         <div>
           <label for="email-address" class="sr-only">Email address</label>
           <input id="email-address" v-model="email" name="email" type="email" autocomplete="email" required class="relative block w-full appearance-none rounded-none rounded-t-md border border-gray-300 px-3 py-2 text-gray-900 placeholder-gray-500 focus:z-10 focus:border-indigo-500 focus:outline-none focus:ring-indigo-500 sm:text-sm" placeholder="Email address">
         </div>
         <div>
           <label for="password" class="sr-only">Password</label>
           <input id="password" name="password" v-model="password" type="password" autocomplete="current-password" required class="relative block w-full appearance-none rounded-none rounded-b-md border border-gray-300 px-3 py-2 text-gray-900 placeholder-gray-500 focus:z-10 focus:border-indigo-500 focus:outline-none focus:ring-indigo-500 sm:text-sm" placeholder="Password">
         </div>
       </div>
 
 
       <div>
         <button type="submit" @click.prevent="submit()" class="group relative flex w-full justify-center rounded-md border border-transparent bg-indigo-600 py-2 px-4 text-sm font-medium text-white hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2">
           <span class="absolute inset-y-0 left-0 flex items-center pl-3">
             <!-- Heroicon name: mini/lock-closed -->
             <svg class="h-5 w-5 text-indigo-500 group-hover:text-indigo-400" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor" aria-hidden="true">
               <path fill-rule="evenodd" d="M10 1a4.5 4.5 0 00-4.5 4.5V9H5a2 2 0 00-2 2v6a2 2 0 002 2h10a2 2 0 002-2v-6a2 2 0 00-2-2h-.5V5.5A4.5 4.5 0 0010 1zm3 8V5.5a3 3 0 10-6 0V9h6z" clip-rule="evenodd" />
             </svg>
           </span>
           Sign up
         </button>
       </div>
     </form>
 
 </div>
   <SignupPage msg="Welcome to Your Vue.js App"/>
   <!-- <vue-basic-alert ref="alert" /> -->
 
 
 </template>
 <script>
 import SignupPage from '@/components/SignupPage.vue';
import { constant ,config} from './constant';
     
     export default {
       name: 'SignupView',
       components: {
     SignupPage,
       },
       data(){
         return {
             name:'',
             email:'',
             password:''
         }
       },
       methods:{
         submit(){
           
            if(!this.name.length){
                 alert("Please fill name");
             }
             if(!this.email.length){
                 alert("Please fill email");
             }
 
             if(!this.password.length){
                 alert("Please fill password");
             }
 
           
 
             config.method="POST";
            config.body=JSON.stringify({name:this.name,email:this.email,password : this.password});

             fetch(constant.BACKEND_URL+'register',config).then(response => {
           if (response.status == 200) {
             return response.json();            
           } else {
             alert(response.statusText);
           }
         }).then(data =>{
                 if(data.access_token){
                   localStorage.setItem('token',data.access_token);
                   window.location.href="/";
                 }
             }).catch()
         }
       }
     }
     </script>