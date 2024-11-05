<script setup>
import { RouterLink, RouterView } from 'vue-router'
import Navbar from './components/Navbar.vue';

</script>
 
<template>
  <div id="Container">
    <Navbar class="Navbar"/>
    <RouterView class="Pages"/>
  </div>
  
</template>


<style scoped>
   #Container{
     background-color: #323e6e;
     display: flex;
     box-shadow: -7px 7px 5px #1b2340;
     border-radius: 10px;
     filter: brightness(1.3);
   }
   .Navbar{
    width: 300px;
    height: 600px;
    background-color: #323e6e;
    border-radius: 10px;
     border-right: 1px solid rgba(213, 213, 213, 0.5);
   }
   .Pages{
    width: 900px;
    height: 600px;
   }
</style>
 
