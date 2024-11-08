<script setup>
const home = "http://localhost:5173"
import { RouterLink } from 'vue-router';
</script>

<template>
    <div>    
        <img class="w-[150px] h-[150px] mt-[30px]" src="../assets/bitcoin.png" alt="Coin">
        <h1 class="text-[26px] font-bold text-[#55f0fa] filter brightness-[2.5] mt-[10px] tracking-[2px]">CryptoWorld</h1>
    <ul class="mt-[40px] w-full">
     <router-link :to="'/'" class="no-underline" active-class="active">
        <li class="flex items-center justify-center mt-[5px] tracking-[2px] w-full h-[40px] text-[#55f0fa] font-[600] text-[16px] bg-[#323e6e]
         hover:text-[#f0f2ee] hover:text-[20px] hover:brightness-[1.3] hover:shadow-[-2px_2px_2px_rgb(29,29,29)]">Home</li></router-link>

     <router-link :to="'/Coins'" class="no-underline" active-class="active">
        <li class="flex items-center justify-center mt-[5px] tracking-[2px] w-full h-[40px] text-[#55f0fa] font-[600] text-[16px] bg-[#323e6e]
         hover:text-[#f0f2ee] hover:text-[20px] hover:brightness-[1.3] hover:shadow-[-2px_2px_2px_rgb(29,29,29)]">Coins</li></router-link>
    </ul>
    </div>
</template>


<style scoped>

.active li{
 filter: brightness(1.3);
 box-shadow: -2px 2px 2px rgb(29,29,29);
}
</style>