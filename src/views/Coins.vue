<script setup>
import CoinsCards from '@/components/CoinsCards.vue';

import { reactive, ref, watch } from 'vue';
import { onMounted } from 'vue';
let data = reactive({
   InfoData: [],
   Isloading: true,
   Isfound: false
});

const temp = reactive({
  data: []
})
let search = ref('');
async function CoinList(){
  const options = {
  method: 'GET',
  headers: {accept: 'application/json', 'x-cg-demo-api-key': 'CG-9PqEUQ87YvbwZyGUYdFNw3eP'}
};

const response = await fetch('https://api.coingecko.com/api/v3/coins/markets?vs_currency=usd', options)
   data.InfoData = await response.json();
   temp.data = data.InfoData;
   data.Isloading = false;
   console.log(data.InfoData);
}
watch(search, ()=>{
   if(search.value!==''){
      let found=true;
       for(let i=0;i<data.InfoData.length;i++){
          if(data.InfoData[i].name.toLowerCase() === search.value.toLowerCase()){
            data.InfoData = data.InfoData[i];
            data.Isfound = true;
             found = false;
             data.Isloading = false;
            break;
           }
       }

       if(found){ 
         data.Isfound = false;
         data.Isloading =true;
         data.InfoData = temp.data;   
       }
   }else{
      data.Isfound = false;
      data.Isloading =false;
      data.InfoData = temp.data;
   }
})


onMounted(() => {
   CoinList();
});

</script>
<template>
  <div class="w-[900px] h-[600px] flex justify-center items-center flex-col">
    <form action="" class="mt-[30px]">
      <input type="text" v-model="search" placeholder="Name of Coin" class=" mb-[20px] w-[600px] h-[40px] rounded-[10px] p-[5px] placeholder-black border filter brightness-[.8] shadow-[-3px_2px_2px_rgb(29,29,29)]">
    </form>
     <div class="grid grid-cols-4 gap-[10px] p-[5px] h-[600px] overflow-y-auto">
      <div v-if="data.Isfound">
        <CoinsCards :data="data.InfoData"/>
      </div>
      <div v-else-if="data.Isloading">
        <h1 class="mt-[30px] text-white text-[30px]">Loading...</h1>
      </div>
      <div v-else @click="ShowCoinInfo" v-for="index in 52" :key="index">
          <CoinsCards :data="data.InfoData[index-1]" class="w-[200px] h-[100px]" />
       </div>
  </div>

  </div>
 
</template>

<style scoped>

.overflow-y-auto::-webkit-scrollbar {
    display: none;
  }

</style>
