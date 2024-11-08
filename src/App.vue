<script setup>
import { RouterLink, RouterView } from 'vue-router'
import Navbar from './components/Navbar.vue';

</script>
 
<template>
  <div class="flex shadow-lg bg-[#323e6e] filter brightness-[1.5] rounded-md">
    <Navbar class="flex flex-col items-center w-[300px] h-[600px] bg-[#323e6e] rounded-[10px]
   border-r-2 border-[rgba(213,213,213,0.5)]"/>
    <RouterView class="w-[900px] h-[600px]"/>
  </div>
</template>


<style scoped>
</style>
 
