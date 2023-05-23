<template>
    <div ref="hero" class="hero">
      <!-- Content of your hero section -->
        
      <h1 ref="title1">Welcome</h1>
      <h1 ref="title2">Lets Find Your Dream Home!</h1>
        <div ref="search_box" class="container">
           
            <div  class="search">
                <input placeholder="Enter city, province or complete address (Canada)" v-model="query" class="search-field" type="text">
                <button class="btn"  @click="searchClicked">Search</button>
            </div>
        </div>
</div>

</template>

<script setup>
import { inject, onMounted, ref } from 'vue';
import  {gsap} from 'gsap';
import { Timeline } from 'gsap/gsap-core';
const query = ref("");
const search= inject('search');
const searchClicked = ()=>{
    console.log("search")
    search(query.value)
}

//Animations
const tl = gsap.timeline({paused:true})
const hero=ref(null)
const title1=ref(null)
const title2=ref(null)
const search_box=ref(null)

onMounted(()=>{
   tl.to(search_box.value, {
    
    opacity: 0,
        duration: 0,
      })
    tl.to(title2.value, {
        display:"none",
    opacity: 0,
        duration: 0,
      })
      tl.to(title1.value, {
        opacity: 1,
        duration: 1.5,
      })
      tl.to(title1.value, {
        display:"none",
        opacity: 0,
        duration: 0.5,

      })
      
    tl.to(title2.value, {
        display:"block",
    opacity: 1,
        duration: 1,
      })
      tl.to(hero.value,{
        height:"25vh",
        duration: 2
      })
      tl.to(search_box.value, {
    
    opacity: 1,
        duration: 0.5,
      })

      
      
      
tl.play()
  
}
  )

</script>


<style scoped>

@import url('https://fonts.googleapis.com/css2?family=Playfair+Display:wght@500&family=Quicksand:wght@300;400;500;600&display=swap');

input{
    text-indent: 2rem;
    font-size: large;
}

h1{
    margin: 3rem 0 ;
    text-align: center;
    outline-width: 3rem;
    color:#ffffff;
    font-weight:  bold;
    outline: black;
    font-family: 'Playfair Display', serif;

}

.hero{

    display: flex;
    flex-direction: column;
    justify-content: center;
   
    background: linear-gradient(rgba(0, 0, 0, 0.2), rgba(0, 0, 0, 0.70)), url("../src/assets/real-estate-bg-2.jpg");
   
    background-color: aqua;
    align-items: center;
    background-position: center;
    background-size: cover;
    height: 100vh;
    
    margin: 0;
}
.search{
    display: flex;
    height: 2rem;
    gap: 1rem;
    align-items: center;
    
    width: 35vw;
}
.search-field{
    width: 100%;
    height: 100%;
    caret-color: auto;
}

.btn {
    background-color: #0ea068;
    
    height: 100%;
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