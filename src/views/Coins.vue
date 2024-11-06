<script setup>
import CoinsCards from '@/components/CoinsCards.vue';
import CoinInfo from '@/components/CoinInfo.vue';

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
  <div class="ParentCont">
    
    <form action="">
      <input type="text" v-model="search" placeholder="Name of Coin">
    </form>
     <div class="CoinsContainer">
      <div v-if="data.Isfound">
        <CoinsCards :data="data.InfoData" />
      </div>
      <div v-else-if="data.Isloading">
        <h1 >Loading...</h1>
      </div>
      <div v-else @click="ShowCoinInfo" v-for="index in 52" :key="index">
          <CoinsCards :data="data.InfoData[index-1]" />
       </div>
  </div>

  </div>
 
</template>

<style scoped>
.ParentCont{
  width: 900px;
  height: 600px;  
  display: flex;
  justify-content: center;
  flex-direction: column;
  align-items: center;
}
.ContainerCards{
  color: white;
   border: 1px solid white;
   display: flex;
   align-items: center;
   justify-content: center;
   background-color: rgb(50, 62, 110, 1.3);
   cursor: pointer;
}

.ContainerCards:hover{
  box-shadow: -2px 2px 2px rgb(29, 29, 29);
  filter: brightness(1.3);
}



.CoinsContainer{
  display: grid;
  grid-template-columns: repeat(4, 200px); 
  grid-auto-rows: 100px;
  gap: 10px;
  padding: 5px;

  height: 600px;

  overflow-y: auto;
  
  }

  .CoinsContainer::-webkit-scrollbar {
  display: none;
}
.CoinsContainer {
  -ms-overflow-style: none; 
  scrollbar-width: none;  
}

form{
   margin-top: 30px;
   
}
input{
  width: 610px;
   height: 40px;
   border-radius: 10px;
   padding: 5px;
   font-size: 15px;
   margin-bottom: 30px;
}

h1{
  color:white;
}

</style>
