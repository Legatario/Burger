<template>
    <div class="wrapper">
      <RouterLink to="/" id="logoUrl">
        <img :src="logo" :alt="alt" id="logo">
      </RouterLink>

      <nav>
        <RouterLink to="/">Home</RouterLink> 
        <RouterLink to="/pedidos">Pedidos</RouterLink>
      </nav>
    </div>
</template>


<script>
    // import { RouterLink, RouterView } from 'vue-router'
    export default{
        name:'Navbar',
        props: ["logo", "alt"]
    }
</script>

<style scoped>
  .wrapper{
    background: #222;
    border-bottom: 4px solid #111;
    padding: 15px 50px;
    display: flex;
    justify-content: flex-end;
    align-items: center;
  }

   #logoUrl{
    margin: auto;
    margin-left: 0;
  }
  #logo{
    width: 40px;
    height: 40px;
  }
  nav a{
    color: #fcba03;
    text-decoration: none;
    margin: 12px;
    transition: .5s;
  }
  nav a:hover{
    color: #fff;
  }
</style>