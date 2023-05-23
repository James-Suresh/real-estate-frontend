<script setup>
import { onMounted, provide } from 'vue';
import axios from 'axios'
import { processExpression } from '@vue/compiler-core'
import Hero from './components/Hero.vue'
import { ref } from 'vue';
import  gsap   from 'gsap';
import Listings from './components/Listings.vue';





const loc = ref({
  latMax: 81.14747595814636,//North East latitute
  lngMax: -10.267941690981388,//North East longitude
  latMin: -22.26872153207163,//South West latitude
  lngMin: -136.83037765324116,//South West longitude
})


const search = async (query) => {

 

  try {
    console.log(query)
    const response = await axios.get("https://maps.googleapis.com/maps/api/geocode/json?address="+query+"&key="+import.meta.env.VITE_APP_GOOGLE_API_KEY)
    console.log(response.data?.results[0]?.geometry?.bounds)
    const bounds = response.data?.results[0]?.geometry?.bounds
    if(bounds)
    {
      loc.value.latMax = bounds.northeast.lat
      loc.value.lngMax = bounds.northeast.lng
      loc.value.latMin = bounds.southwest.lat
      loc.value.lngMin = bounds.southwest.lng
    }
    
  } catch (error) {
    console.error(error)
    
  }
}

provide ("search", search)


//Animations

const container = ref(null)
// onMounted(()=>{
//     gsap.from(container.value, {
//         opacity: 0,
//         duration:1,
        
//       });
//   })
</script>
<template>
  <div ref="container">
    <Hero/>
    <Listings v-bind:loc="loc" />
  </div>
</template>
