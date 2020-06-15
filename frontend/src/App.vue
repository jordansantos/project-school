<template>
  <div id="app">
    <Nav/>
    <div class="margem_principal">
      <router-view :key="$route.fullPath"></router-view>
    </div>
  </div>
</template>

<script>
import Nav from './components/_nav/Nav'

export default {
  name: 'App',
  components: {
    Nav
  }
}
</script>

<style>
  @import url("https://fonts.googleapis.com/css?family=Montserrat:400,700");
  
  body { 
    background-color: #eee; 
    display: grid;
    font-family: "Montserrat", sans-serif;
    justify-items: center; 
  }

  body, html { 
    height: 100%;
    margin: 0;
  }
  
  .margem_principal { 
    margin: auto;
    width: 50%;
  }
  
  #app {
    width: 100%;
  }
  
  .btn_danger {
    background-color: #fa4430;
    font-size: 0.8em !important;
  }
  
  .btn {
    border: 1px solid #000;
    border-bottom: 3px solid #000;
    border-radius: 5px;
    color: rgb(255, 253, 253);
    cursor: pointer;
    font-size: 1.2em;
    font-weight: bold;
    padding: 10px 20px;
  }
  
  .btn:hover {
    border-bottom: 1px solid #000;
    margin-top: 3px;
    text-shadow: 1px 1px 1px #000;
  }

  table { 
    list-style-type: none;
    margin: 0px;
    padding: 0px;
    width: 100%;
  }
  table tr, td { 
    background-color: #e0edf4;
    color: #3e5252;
    font-size: 1.3em;
    padding: 20px;
    margin-bottom: 2px;
  }
  
  table thead th { 
    background-color: rgb(184, 208, 216) !important; 
    font-size: 1.2em; 
    padding: 10px 0px; 
    text-align: center !important;
  }
  
  .colPequeno { 
    background-color: rgb(125, 217, 245); 
    font: bold;
    text-align: right;
    width: 5%; text-align: right;
  }
</style>
