<script setup>
import { defineProps } from 'vue';


const props  = defineProps({
    data: {
         type: Object,
        default: []
    }
})
console.log(props.data.market_cap_rank);
</script>

<template>
    <div class="ContainerHome">
         <span># {{ props.data.market_cap_rank }}</span>
             <img v-bind:src="props.data.image" alt="Coin">
         <span class="CoinNameCont">{{ props.data.name }}</span>
        <span class="CoinSymbolCont">
            {{ props.data.symbol }}
        </span>
         <span class="Price">$ {{ props.data.current_price }}</span>
    </div>
</template>

<style scoped>

.ContainerHome{
    display: flex;
    font-weight: 500;
   padding: 10px;
    font-size: 20px;
    background-color: #2b3662;
    align-items: center;
    width: 500px;
    color: #f0f2ee;
    border: 1px  solid rgba(131, 131, 131, 0.5);
    box-shadow: -2px 2px 2px rgb(29, 29, 29);
}
.CoinNameCont{
   height: 100%;
   width: 140px;
}
.CoinSymbolCont{
   height: 100%;
   width: 60px;
}
img{
    width: 50px;
    height: 50px;
    margin-left: 20px;
    margin-right: 20px;
}

.Price{
    margin-left: 50px;
}
</style>