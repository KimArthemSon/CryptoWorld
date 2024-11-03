<script setup>

</script>


<template>
    <div class="ContainerHome">
         <span>1</span>
         <img src="../assets/bitcoin.png" alt="Coin">
         <span>Bitcoin</span>
         <span>$20,000.00</span>
    </div>
</template>

<style scoped>

.ContainerHome{
    display: flex;
   justify-content: space-between;
    font-weight: 500;
   padding-left: 20px;
   padding-right: 20px;
    font-size: 20px;
    background-color: #2b3662;
    align-items: center;
    width: 500px;
    color: #f0f2ee;
    border: 1px  solid rgba(131, 131, 131, 0.5);
    box-shadow: -4px 4px 4px rgb(29, 29, 29);
}

img{
    width: 50px;
    height: 50px;
}
</style>