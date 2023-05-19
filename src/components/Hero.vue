<template>
    <div class="hero">
      <!-- Content of your hero section -->

      <h1>Lets Find Your Dream Home!</h1>
        <div class="container">
           
            <div class="search">
                <input placeholder="Enter city, province or complete address (Canada)" v-model="query" class="search-field" type="text">
                <button class="btn"  @click="searchClicked">Search</button>
            </div>
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
input{
    text-indent: 2rem;
    font-size: large;
}
.container{
    padding: 0rem 2rem;
    border-radius: 0.25rem;
    background-color: rgba(255, 255, 255, 0.7);
}
h1{
    margin: 3rem 0 1.5rem ;
    text-align: center;
    outline-width: 3\5rem;
    color:#bcffe5;
    font-weight:  bold;
    outline: black;


}

.hero{

    display: flex;
    flex-direction: column;
    justify-content: center;
   
    background: linear-gradient(rgba(0, 0, 0, 0.2), rgba(0, 0, 0, 0.50)), url("src/assets/real-estate-bg.jpg");
   
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
    
    width: 50vw;
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