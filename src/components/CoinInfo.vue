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
const coin = ref(1); 
const currency = ref(coin.value * (props.data.current_price || 0)); 


watch(coin, (newCoin) => {
    currency.value = newCoin * (props.data.current_price || 0);
});

watch(currency, (newCurrency) => {
    if (props.data.current_price) {
        coin.value = newCurrency / props.data.current_price;
    }
});
/*async function fetchCurrency(){
  const response = await fetch('https:/api.exchangerate-api.com/v4/latest/usd');
  const currency =await response.json();
  currency.value = currency.rates.USD;
  console.log(currency)
}*/

</script>


<template>
    <div class="ParentInfoCont">
      <div class="InfoCaoinCont">
         <div class="CoinInfo">
             <h1>$ {{ props.data.current_price }}</h1> 
             <div class="NameCoin">
                <img v-bind:src="props.data.image" alt="Coin">
                <span>{{ props.data.name }}</span>
                <span># {{ props.data.market_cap_rank }}</span>
             </div> 
           <div class="AboutCoin">
               <span class="CoinAbout">About</span>
                <h4>High_24h: <span>  {{ props.data.high_24h }}</span></h4>
                <h4>low_24h: <span>  {{ props.data.low_24h }} </span></h4>
                <h4>price_change_24h: <span>  {{ props.data.price_change_24h }} </span></h4>
                <h4>Total_volume: <span>  {{ props.data.total_volume }} </span></h4>
                <h4>Total_supply: <span>  {{ props.data.total_supply }} </span></h4>
          </div>
         </div>
         <div class="CoinConverter">
            <span @click="props.toggleInfo" class="close">x</span>
             <h2>Bitcoin Converter</h2>
            <input type="number" min="0" v-model="coin" placeholder="Bitcoin" >
            <input type="number" min="0" v-model="currency" placeholder="Usd">
            <span class="currency-label">USD Currency</span>
         </div>
        </div>
    </div>
  
</template>

<style scoped>
.ParentInfoCont{
  position: absolute;
  z-index: 2;
  width: 870px;
  left: 25%;
  top: 100px;
}
.InfoCaoinCont{
   display: flex;
    width: 900px;
    height: 500px;
    border: 1px solid rgb(255, 255, 255, .5);
    background-color: rgb(50, 62, 110);
    filter: brightness(.9);
    box-shadow: -3px 3px 3px rgb(29, 29, 29);
}
.close{
    cursor: pointer;
}
.CoinInfo{
    height: 100%;
    width: 570px;
    border-right: 1px solid rgb(255, 255, 255, .8);
}


.CoinInfo h1{
    margin-bottom: 10px;
    font-size: 35px;
}


.CoinConverter{
    height: 100%;
    width: 320px;
    display: flex;
    flex-direction: column;
   align-items: center;
}

input[type=number]::-webkit-outer-spin-button,
input[type=number]::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}

.CoinConverter > span:nth-child(1){
  color: white;
  margin-left: 290px;
  font-size: 30px;
  margin-bottom: 4px;
}

.CoinConverter .currency-label{
  color: white;
  font-size: 20px;
  margin-top: 10px;
}

.CoinConverter h2{
  color: #55f0fa;
 margin-top: 30%;
}

.CoinConverter input{
   width: 220px;
   font-size: 15px;
   padding: 2px;
   margin-top: 10px;
   background-color: rgb(255, 255, 255, .8);
}
.NameCoin{
    display: flex;
    align-items: center;
    gap: 10px;
}

.NameCoin span:nth-child(1){
  color: #55f0fa;
}


.CoinInfo{
    color: white;
    display: flex;
    flex-direction: column;
    padding: 10px;
}
.CoinInfo img{
    width: 50px;
    height: 50px;
}

.CoinInfo h1{
    margin-top: 50px;
    letter-spacing: 5px;
}
.AboutCoin{
    margin-top: 25px;
    display: flex;
    flex-direction: column;
    overflow-y: auto;
}
.AboutCoin .CoinAbout{
    background-color: #2b3662;
    color: #f0f2ee;
    font-size: 20px;
    filter: brightness(1.3);
    padding: 10px;
    box-shadow: -2px 2px 2px rgb(29, 29, 29);
}

.AboutCoin h4{
    background-color: #2b3662;
    color: #f0f2ee;
    padding: 25px;
    box-shadow: -2px 2px 2px rgb(29, 29, 29);
    margin-top: 14px;
    letter-spacing: 2px;
}

.AboutCoin span{
  color: #55f0fa;
}
</style>