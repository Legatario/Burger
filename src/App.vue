<template>
    <Navbar :logo="logo_src" :alt="alt_src"/>
    <RouterView />
    <Footer />  
</template>

<script>
  import Navbar from './components/Header/Navbar.vue';
  import Footer from './components/Footer/Footer.vue';
  // import { RouterLink, RouterView } from 'vue-router'
  export default{
    components:{
      Navbar,
      Footer
    },
    data(){
      return{
        logo_src: "/img/logo.png",
        alt_src: "Burguer Burguer"
      }
    }
  }
</script>


<style>
  *{
    font-family: Arial, Helvetica, sans-serif;
    padding: 0;
    margin: 0;
    box-sizing: border-box;
  }
  .main_container{
    margin: 50px;
    min-height: 36vw;
  }
  h1{
    text-align: center;
    font-size: 42px;
    margin-bottom: 30px;
    color: #222;
  }
</style>
