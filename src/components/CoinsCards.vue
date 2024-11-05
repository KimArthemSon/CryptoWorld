<script setup>
import { defineProps } from 'vue';
import CoinInfo from './CoinInfo.vue';
import { ref } from 'vue';
const props = defineProps({
    data: {
      type: Object,
      default: []
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
      <div class="ContainerCards"  @click="ShowCoinInfo2">
        <img v-bind:src="props.data.image" alt="Coin">
    <div class="infoCard">
      <span>$ {{ props.data.current_price }}</span>
      <span>{{ props.data.name }}</span>
    </div>
      </div>
     
</template>

<style scoped>

.ContainerCards{
  color: white;
   border: 1px solid white;
   display: flex;
   width: 100%;
   height: 100%;
   align-items: center;
   justify-content: center;
   background-color: rgb(50, 62, 110, 1.3);
   cursor: pointer;
}

.ContainerCards:hover{
  box-shadow: -2px 2px 2px rgb(29, 29, 29);
  filter: brightness(1.3);
}

.infoCardCont{
  display: flex;
}
img{
    width: 50px;
    height: 50px;
    margin-right: 5px;
}
 .infoCard{
    display: flex;
    flex-direction: column;
}
.infoCard span:nth-child(2){
  color: #55f0fa;
}



</style>