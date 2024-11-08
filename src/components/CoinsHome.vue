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
    <div class="flex items-center flex-row hover:brightness-[1.3] 
    font-[500] p-[10px] text-[20px] bg-[rgb(43,54,98)] w-[500px] text-[#f0f2ee] border-[1px]
     border-[rgba(255,255,255,.3)] shadow-[-2px_2px_2px_rgb(29,29,29)]">

         <span># {{ props.data.market_cap_rank }}</span>
             <img v-bind:src="props.data.image" alt="Coin" class="w-[50px] h-[50px] ml-[20px] mr-[20px]">
         <span class="h-full w-[140px]">{{ props.data.name }}</span>
        <span class="h-full w-[60px]">
            {{ props.data.symbol }}
        </span>
         <span class="ml-[50px]">$ {{ props.data.current_price }}</span>
    </div>
</template>

<style scoped>

</style>