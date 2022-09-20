<template >
  
  <Navbar :isLoggedIn=this.isLoggedIn />
  <router-view />
  <Footer />
</template>

<script>
import Navbar from './components/Navbar'
import Footer from './components/Footer'
export default {
  name: 'App',
  components: {
    Navbar,
    Footer,
  },
  data(){
    return {
      isLoggedIn : false
    }
    
  },
  created(){
    if(localStorage.getItem('token')){
      this.isLoggedIn = true;
    }
  },
  methods: {
    logout(){
      localStorage.removeItem('token')
      window.location.href ='/login'
    }
    
  }
  
 
  
}
</script>


