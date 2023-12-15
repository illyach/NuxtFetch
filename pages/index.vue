<template>
  <div class="container">


    <NuxtLink to="/products">
      LOAD PRODUCTS 
    </NuxtLink>

        <div class="hidden_text">
    <p>The greatest glory in living lies not in never falling, 
      but in 
    </p>

    <p @click="textClick()" v-if="state" class="continue">Click here to continue</p>

    <p v-if="!state">rising every time we fall
    </p>
  </div>
</div>
</template>

<script setup>
const state = ref(true)
const textClick = () => {
  state.value = !state.value
}
</script>

<style scoped>
a{
  margin-top: 10px;
  font-size: 60px;
  color:rgb(95, 197, 95);
  margin-top: 5px;
  margin: 10px 0 0 0;
  display: flex;
  justify-content: center;
  align-items: center;
}
.hidden_text{
  position: relative;
  top:120px;
}
p{
  margin-top: 10px;
  font-size: 60px;
  color:white;
  margin-top: 5px;
  margin: 10px 0 0 0;
  display: flex;
  justify-content: center;
  align-items: center;
}
.continue{
  color:rgb(95, 197, 95);
}
.container{
  background-color: black;
  position: absolute;
height: 100%;
  width: 100%;

}
</style>