<template>
  <main class="main_container">
      <h1>Gerenciar pedidos</h1>
      <Dashboard />
  </main>
</template>


<script>
import Dashboard from '../components/Pedidos/Dashboard.vue';
  export default{
    name: "Pedidos",
    
    components: { 
      Dashboard 
    }
}
</script>