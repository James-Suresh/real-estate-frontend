<template>
    <div class="hero">
      <!-- Content of your hero section -->
    
        <div class="search">
            <input placeholder="Enter address" v-model="query" class="search-field" type="text">
            <button class="btn"  @click="searchClicked">Search</button>
        </div>
</div>

</template>

<script setup>
import { inject, ref } from 'vue';

const query = ref("");
const search= inject('search');
const searchClicked = ()=>{
    console.log("search")
    search(query.value)
}
</script>

<style scoped>
.hero{
    display: flex;
    justify-content: center;
    background-image: url("src/assets/real-estate-bg.jpg");
    background-color: aqua;
    align-items: center;
    background-position: center;
    background-size: cover;
    height: 30rem;
    
    margin: 0;
}
.search{
    display: flex;
    height: 5rem;
    gap: 1rem;
    align-items: center;
    padding: 2rem;
    width: 50vw;
    background-color: rgba(0, 0, 0, 0.3);
}
.search-field{
    width: 100%;
    height: 2rem;
}

.btn {
    background-color: #0ea068;
    
    height: 2rem;
    color: #fff;
    text-transform: uppercase;
    letter-spacing: 2px;
    cursor: pointer;
    border: 2px dashed #0ea068;
    box-shadow: rgba(50, 50, 93, 0.25) 0px 2px 5px -1px, rgba(0, 0, 0, 0.3) 0px 1px 3px -1px;
    transition: .4s;
   }
   
   .btn span:last-child {
    display: none;
   }
   
   .btn:hover {
    transition: .4s;
    border: 2px dashed rebeccapurple6;
    background-color: #fff;
    color: #17FBA2;
   }
   
   .btn:active {
    background-color: #87dbd0;
   }
  
</style>