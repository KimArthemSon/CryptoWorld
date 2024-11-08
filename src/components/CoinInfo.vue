<script setup>
import { defineProps, computed,ref,watch} from 'vue';

const props = defineProps({
    data: {
      type: Object,
      default: []
    },
    toggleInfo: {
        type: Function
    }
})
const coin = ref(1.00); 
const currency = ref(coin.value * (props.data.current_price || 0.00)); 

let CoinWatch = ()=>{};

let USDwatch = ()=>{};

function CoinORusd(ident){
if(!ident){
  Coinsy();
}
else{ 
USD();
}
}
function USD(){
   CoinWatch();
    USDwatch = watch(currency, (newCurrency) => {
    if (props.data.current_price) {
        coin.value = newCurrency / props.data.current_price;
    }
});
 }
function Coinsy(){
    USDwatch();
CoinWatch = watch(coin, (newCoin) => {
  console.log("hello")
    currency.value = newCoin * (props.data.current_price || 0.00);
});

}


/*async function fetchCurrency(){
  const response = await fetch('https:/api.exchangerate-api.com/v4/latest/usd');
  const currency =await response.json();
  currency.value = currency.rates.USD;
  console.log(currency)
}*/

</script>


<template>
    <div class=" absolute z-3 w-[890px] left-[25%] top-[90px]">
      <div class="flex w-[900px] h-[510px] border-2 border-[rgb(255,255,255,.5)] bg-[rgb(50,62,110)] 
      filter brightness-[.9] shadow-[-3px_3px_3px_rgb(29,29,29)]">
         <div class="p-[10px] h-full w-[570px] border-r-2 border-[solid rgb(255, 255, 255, .8)]">
             <h1 class="mb-[10px] mt-[30px] tracking-[5px] text-[35px] text-white">$ {{ props.data.current_price }}</h1> 
             <div class="flex items-center gap-[10px]">
                <img v-bind:src="props.data.image" alt="Coin" class="w-[50x] h-[50px]">
                <span class="text-[#55f0fa] text-[18px] font-[600]">{{ props.data.name }}</span>
                <span class="text-white text-[18px] font-[600]"># {{ props.data.market_cap_rank }}</span>
             </div> 
           <div class="flex flex-col w-full h-[320px] overflow-y-auto mt-[25px]">
               <span class="bg-[#2b3662] text-[20px] filter brightness-[1.3] p-[10px] shadow-[-2px_2px_2px_rgb(29,29,29)] text-[#55f0fa] w-[80px] text-center font-bold ">About</span>
                <h4 class="bg-[#2b3662] text-[#f0f2ee] p-[25px] shadow-[-2px_2px_2px_rgb(29,29,29)] mt-[14px] tracking-[2px]">High_24h: <span class="text-[#55f0fa]">  {{ props.data.high_24h }}</span></h4>
                <h4 class="bg-[#2b3662] text-[#f0f2ee] p-[25px] shadow-[-2px_2px_2px_rgb(29,29,29)] mt-[14px] tracking-[2px]">low_24h: <span class="text-[#55f0fa]">  {{ props.data.low_24h }} </span></h4>
                <h4 class="bg-[#2b3662] text-[#f0f2ee] p-[25px] shadow-[-2px_2px_2px_rgb(29,29,29)] mt-[14px] tracking-[2px]">price_change_24h: <span class="text-[#55f0fa]">  {{ props.data.price_change_24h }} </span></h4>
                <h4 class="bg-[#2b3662] text-[#f0f2ee] p-[25px] shadow-[-2px_2px_2px_rgb(29,29,29)] mt-[14px] tracking-[2px]">Total_volume: <span class="text-[#55f0fa]">  {{ props.data.total_volume }} </span></h4>
                <h4 class="bg-[#2b3662] text-[#f0f2ee] p-[25px] shadow-[-2px_2px_2px_rgb(29,29,29)] mt-[14px] tracking-[2px]">Total_supply: <span class="text-[#55f0fa]">  {{ props.data.total_supply }} </span></h4>
          </div>
         </div>
         <div class="h-full w-[320px] flex flex-col items-center">
            <span @click="props.toggleInfo" class=" cursor-pointer text-[white] ml-[290px] text-[30px] mb-[4px]">x</span>
             <h2 class="text-[#55f0fa] mt-[30%] text-[20px] font-bold tracking-[3px]">Bitcoin Converter</h2>
            <input type="number" min="0" v-model="coin" v-on:focus="CoinORusd(false)" placeholder="Bitcoin"  class=" placeholder-[black] w-[220px] text-[15px] p-[5px] mt-[10px]  border border-gray-300 rounded-lg  text-black font-bold focus:outline-none focus:border-blue-500 focus:ring-1 focus:ring-blue-500">
            <input type="number" min="0" v-model="currency" v-on:focus="CoinORusd(true)" placeholder="USD" class="placeholder-[black] w-[220px] text-[15px] p-[5px] mt-[10px] border border-gray-300 rounded-lg text-black font-bold focus:outline-none focus:border-blue-500 focus:ring-1 focus:ring-blue-500">
            <span class="text-[white] text-[20px] mt-[10px]">USD Currency</span>
         </div>
        </div>
    </div>
  
</template>

<style scoped>

input[type=number]::-webkit-outer-spin-button,
input[type=number]::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}

</style>