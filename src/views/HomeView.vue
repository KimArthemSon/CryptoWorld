<script setup>
import Coins from '@/components/CoinsHome.vue';
import { RouterLink } from 'vue-router';
import { reactive, ref, onMounted,computed, watch } from 'vue';

const data = reactive({
   InfoData: [],
   Isloading: true,
   found: false
});
const temp = reactive({
  data: []
})
const search = ref(''); 

async function CoinList() {
  const options = {
    method: 'GET',
    headers: {
      accept: 'application/json',
      'x-cg-demo-api-key': 'CG-9PqEUQ87YvbwZyGUYdFNw3eP'
    }
  };

  const response = await fetch('https://api.coingecko.com/api/v3/coins/markets?vs_currency=usd', options);
  data.InfoData = await response.json();
  temp.data = data.InfoData;
  data.Isloading = false;
}
watch(search, ()=>{
   if(search.value!==''){
      let found=true;
       for(let i=0;i<data.InfoData.length;i++){
          if(data.InfoData[i].name.toLowerCase() === search.value.toLowerCase()){
            data.InfoData = data.InfoData[i];
            data.found = true;
             found = false;
             console.log("hello")
            break;
           }
       }

       if(found){ 
         data.found = false;
         data.InfoData = temp.data;
       }
   }else{
      data.found = false;
      data.InfoData = temp.data;
   }
})
onMounted(() => {
  CoinList();
});
</script>

<template>
   <div class="flex items-center flex-col">
      <h1 class="text-[#55f0fa] filter brightness-[2] text-[40px] mt-[30px] font-bold">Crypto Coins</h1>
      <input type="text" v-model="search" placeholder="Name of Coin"
      class="mt-[30px] mb-[20px] w-[600px] h-[40px] rounded-[10px] p-[5px] placeholder-black border filter brightness-[.8] shadow-[-3px_2px_2px_rgb(29,29,29)]">
      
      <div v-if="!data.Isloading && search === '' " v-for="index in 5" :key="index">
        <router-link to="/Coins" class="no-underline">
          <Coins :data="data.InfoData[index - 1]" class="cursor-pointer hover:shadow-[-4px_4px_4px_rgb(29,29,29)]"/>
        </router-link>
      </div>
      <div v-else-if="data.found">
         <router-link to="/Coins" class="no-underline">
          <Coins :data="data.InfoData" class="cursor-pointer hover:shadow-[-4px_4px_4px_rgb(29,29,29)]"/>
        </router-link>
      </div>
      <div v-else>
         <h1 class="text-white text-[30px]">Loading...</h1>
      </div>

      <router-link to="/Coins"><button class="mt-[10px] p-[7px] text-[black] cursor-pointer shadow-[-3px_2px_2px_rgb(29,29,29)] bg-[white]
         transition-transform duration-150 transform hover:scale-105 active:scale-95 focus:outline-none">View More</button></router-link>
   </div>
</template>



<style scoped>

</style>
