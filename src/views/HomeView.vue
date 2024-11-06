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
   <div class="Container">
      <h1>Crypto Coins</h1>
      <input type="text" v-model="search" placeholder="Name of Coin">
      
      <div v-if="!data.Isloading && search === '' " v-for="index in 5" :key="index">
        <router-link to="/Coins" class="Link">
          <Coins :data="data.InfoData[index - 1]" class="Coins"/>
        </router-link>
      </div>
      <div v-else-if="data.found">
         <router-link to="/Coins" class="Link">
          <Coins :data="data.InfoData" class="Coins"/>
        </router-link>
      </div>
      <div v-else>
         <h1>Loading...</h1>
      </div>

      <router-link to="/Coins"><button>View More</button></router-link>
   </div>
</template>



<style scoped>
h1 {
   color: #55f0fa;
   filter: brightness(2);
   font-size: 40px;
   margin-top: 40px;
}

.Container {
   display: flex;
   align-items: center;
   flex-direction: column;
}

input {
   margin-top: 30px;
   width: 600px;
   height: 40px;
   border-radius: 10px;
   padding: 5px;
   font-size: 15px;
   margin-bottom: 30px;
}

.Link {
   text-decoration: none;
}

button {
   margin-top: 10px;
   padding: 7px;
   color: black;
   cursor: pointer;
   box-shadow: -3px 2px 2px rgb(29, 29, 29);
}

.Coins:hover {
   filter: brightness(1.3);
   cursor: pointer;
   box-shadow: -4px 4px 4px rgb(29, 29, 29);
}
</style>
