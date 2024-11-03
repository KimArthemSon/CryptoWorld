<script setup>
import Coins from '@/components/CoinsHome.vue';
</script>

<template>
   <div class="Container">
      <h1>Crypto Coins</h1>
      <form action="">
         <input type="text" placeholder="Name of Coin">
      </form> 
      <Coins class="Coins"/>
      <Coins class="Coins"/>
      <Coins class="Coins"/>
      <Coins class="Coins"/>
      <Coins class="Coins"/>
      <Coins class="Coins"/>
      <button>View More</button>
   </div>
</template>

<style scoped>
h1{
   color: #55f0fa;
   filter: brightness(2);
   font-size: 40px;
   margin-top: 40px;
}
.Container{
   display: flex;
   align-items: center;
   flex-direction: column;
}
form{
   margin-top: 30px;
   
}
input{
  width: 600px;
   height: 40px;
   border-radius: 10px;
   padding: 5px;
   font-size: 15px;
   margin-bottom: 30px;
}

button{
   margin-top: 30px;
   padding: 7px;
   color: black;
   cursor: pointer;
   box-shadow: -3px 2px 2px rgb(29, 29, 29);
}
.Coins:hover{
    filter: brightness(1.3);
    cursor: pointer;
}
</style>