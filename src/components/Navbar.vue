<script setup>
const home = "http://localhost:5173"
import { RouterLink } from 'vue-router';
</script>

<template>
    <div class="Container">    
        <img src="../assets/bitcoin.png" alt="Coin">
        <h2>CryptoWorld</h2>
    <ul>
     <router-link :to="'/'" class="links"><li>Home</li></router-link>
     <router-link :to="'/Coins'" class="links"><li>Coins</li></router-link>
    </ul>
    </div>
</template>


<style scoped>
  .Container{
    text-align: center;
    
  }
ul{
    margin-top: 40px
}
ul li{
        width: 100%;
        height: 40px;
        color: #55f0fa;
        font-weight: 600;
        font-size: 16px; 
        display: flex;
        align-items: center;
        justify-content: center;
        margin-top: 5px;
        letter-spacing: 2px;
}
ul li:hover{
    background-color: #2b3662;
    color: #f0f2ee;
    font-size: 20px;
    filter: brightness(1.3);
}
  h2{
        color: #55f0fa;
        filter: brightness(2.5);
        margin-top: 10px; 
        letter-spacing: 2px;
    }

    img{
        width: 150px;
        height: 150px;
        margin-top: 30px;
    }

</style>