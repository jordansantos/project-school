<template>
  <div class="barra_topo">
    <nav class="margem_principal">
      <router-link to="/professores">Professores</router-link>
      <router-link to="/alunos">Alunos</router-link>
      <router-link to="/sobre">Sobre</router-link>
    </nav>
  </div>
</template>

<script>
  export default {
    
  }
</script>

<style scoped>
  nav { 
    padding: 20px 20px 20px 0; 
  }
  
  nav a {
    background-color: #fff;
    border-radius: 3px;
    color: rgb(0, 110, 255);
    font-weight: bold;
    margin-right: 15px;
    padding: 10px;
    text-decoration: none;
  }
  
  nav .router-link-active{
    background-color: rgb(160, 160, 160);
    color: white 
  }
  
  .barra_topo { 
    background-color: rgb(230, 230, 230); 
  }
</style>