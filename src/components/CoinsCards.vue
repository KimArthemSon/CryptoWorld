<script setup>
import { defineProps } from 'vue';
import CoinInfo from './CoinInfo.vue';
import { ref } from 'vue';
const props = defineProps({
    data: {
      type: Object,
      default: {}
    }
})

const toggleInfo = ref(false);
function ShowCoinInfo2(){
    toggleInfo.value = true;  
}

function ShowCoinInfo(){
    toggleInfo.value = false;  
}

</script>

<template>
      <CoinInfo :data="props.data" v-if="toggleInfo" :toggleInfo="ShowCoinInfo"/> 
      <div v-else class="flex items-center justify-center text-[white] border-2 border-white h-[100px] w-[200px] bg-[rgb(50, 62, 110, 1.3)] cursor-pointer
      hover:shadow-[-2px_2px_2px_rgb(29,29,29)] hover:brightness-[1.1] bg-[#323e6e]"
      @click="ShowCoinInfo2">
        <img v-bind:src="props.data.image" alt="Coin" class="w-[50px] h-[50px] mr-[5px]">
    <div class="flex flex-col">
      <span>$ {{ props.data.current_price }}</span>
      <span class="text-[#55f0fa]">{{ props.data.name }}</span>
    </div>
      </div>
</template>

<style scoped>
</style>