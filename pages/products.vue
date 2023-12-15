<template>

    <button @click="twoActions()">refresh page</button>
    <div v-if="pending" class="loading">
        <h1>Loading...</h1>
      </div>
      
    <div v-else class="absoluted" >

        <div class="container">
            <NuxtLink to="/" class="home">
                Home link
              </NuxtLink>
              
                <div v-for="product in productInfo.minProducts" class="wrapper" v-if="!state">
                    <img :src="product.image" alt=""/>
                    <h2>{{product.title}}</h2>
                </div>

                <div v-for="product in productInfo.maxProducts" class="wrapper" :key="productInfo.maxProducts.id" v-if="state" >
                    <img :src="product.image" alt=""/>
                    <h2>{{product.title}}</h2>
                </div>

                <div v-if="!state">
                    <p class="view_all" @click="handleClick()">View all</p>
                </div>
               
        </div>

    </div>
    
     


</template>

<script setup>
const { pending, data: productInfo , refresh} = useAsyncData(
    "productInfo", 
    async () => {
    // let myLimit = 5;

    const [minProducts, maxProducts] = await Promise.all([
        $fetch(`${baseUrl}?limit=${5}`), 
        $fetch(`${baseUrl}?limit=${25}`), 
        // $fetch('https://fakestoreapi.com/products/categories')
    ]);

const maxFilter = () => {
    return maxProducts.filter((item) => item.id > 5)
}

        return {
            minProducts,
            maxProducts
        }
    },  
            {
            lazy:false,
            }
);

const twoActions  = () => {
    refresh()
    state.value = false
}

const baseUrl = 'https://fakestoreapi.com/products';
const state = ref(false)

const handleClick = () => {
   state.value = !state.value
}

onMounted(() => {

})

// const {pending, data:products, refresh} = await useFetch(
//     "https://fakestoreapi.com/products",
//     {
//         lazy:false,
      
//     }
// );

// const {pending, data:products} = await useFetch(
//     "https://fakestoreapi.com/products/1",
//     {
//         lazy:false,
//         pick:["id", "image", "title"]
//     }
// );
</script>

<style  scoped>

.absoluted{

    top: 0;
    left: 0;
    right: 0;
    bottom: 0;

}
.container{
    position: relative;
    display: grid;
    grid-template-columns: repeat(5,1fr);
    gap:30px;
    font-size: 10px;
    padding: 50px;
  
}
.wrapper{
    display: flex;
    text-align: center;
    flex-direction: column;
    justify-content: space-between;
    border-radius: 10px;
    padding: 10px;
    background: rgb(250, 251, 251);
    box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06); 
}

img{
    width: 150px;
    height: 150px;
    align-self: center; 
}
.view_all{
    position: absolute;
    bottom: 0;
    left: 750px;
   font-size: 30px;
   color:rgb(250, 249, 249);
    border: 1px solid white;
    border-radius: 5px;
}

.home{
   position: absolute;
   left:50px;
   font-size: 30px;
   color:white;
   opacity: 80%;
}


.loading{
    
text-align: center;
   font-size: 30px;
   color:rgb(4, 4, 4);

}

button{

background-color:rgb(185, 70, 70);
color:white;
position: absolute;
left: 240px;
float: right;
top:6px;
padding: 5px;
border-radius: 10px;
margin: 0 auto;
font-weight: bold;
z-index: 1;
}

</style>