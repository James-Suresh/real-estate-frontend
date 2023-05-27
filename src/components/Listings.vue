<script setup>
import axios from 'axios'
import { ref, watch, computed, onMounted, onUnmounted, onBeforeUnmount, onUpdated, onBeforeUpdate } from 'vue'
import Card from './Card.vue'
import Loading from './Loading.vue'
import Hero from './Hero.vue'
import {gsap} from 'gsap'

//Variables
const houses = ref(Array(5))
const props = defineProps({
  loc: Object
})
const isFetching = ref(true)
const list_loc = ref(props.loc)
const options = ref({
  method: 'GET',
  url: 'https://realty-in-ca1.p.rapidapi.com/properties/list-residential',
  params: {
    LatitudeMax: list_loc.value.latMax,
    LatitudeMin: list_loc.value.latMin,
    LongitudeMax: list_loc.value.lngMax,
    LongitudeMin: list_loc.value.lngMin,
    CurrentPage: '1',
    RecordsPerPage: '10',
    SortOrder: 'A',
    SortBy: '6',
    CultureId: '1',
    NumberOfDays: '0',
    BedRange: '0-0',
    BathRange: '0-0',
    PriceMin: '251780',
    RentMin: '0',
    BuildingTypeId: '1',
    TransactionTypeId: '2'
  },
  headers: {
    'X-RapidAPI-Key': import.meta.env.VITE_APP_API_KEY,
    'X-RapidAPI-Host': import.meta.env.VITE_APP_API_HOST
  }
})

//Fetching Data
const fetchProperties = async () => {
  try {
    isFetching.value = true
    const response = await axios.request(options.value)
    console.log(response.data)
    houses.value = response.data.Results.map((result) => ({
      price: result.Property.Price,
      address: result.Property.Address?.AddressText.split('|')[0],
      link: 'https://www.realtor.ca/' + result.RelativeDetailsURL,
      image: result.Property.Photo[0]?.MedResPath
    }))
    isFetching.value = false
  } catch (error) {
    console.error(error)
  }
}
fetchProperties()

//Checking if search had changed location info. If location info changed function will make another fetch based on new location.
watch(list_loc.value, (newValue, oldValue) => {
  console.log('change')
  const { latMax, latMin, lngMin, lngMax } = list_loc.value

  options.value.params = {
    ...options.value.params,
    LatitudeMax: latMax,
    LatitudeMin: latMin,
    LongitudeMin: lngMin,
    LongitudeMax: lngMax
  }

  fetchProperties()
})


//Animations
const cards = ref(null)
const tl = gsap.timeline()

function animateList(el){
  onMounted(()=>{
    tl.from(cards.value,{
    duration: 1,
      opacity: 0,
      x: -50,
      stagger: 0.5, // Time delay between each element
  })

 

})

onUpdated(()=>{
  tl.from(cards.value,{
    duration: 1,
      opacity: 0,
      x: -50,
      stagger: 0.5, // Time delay between each element
  })
  })
}
animateList(cards)



</script>

<template>
  <div ref="container" class="listings">
    <h1 class="listings-title">Listings</h1>

    <Loading class="loading" v-if="isFetching" />

    <div ref="cards" v-else v-for="(house, index) in houses" :key="index" :house="house">
  
        <Card    
    :image="house.image"
    :price="house.price"
    :address="house.address"
    :link="house.link"
    />

      
    </div>
  </div>
</template>
<style scoped>
.listings {
  width: 100vw;
  height: 75vh;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 2rem;
  padding: 1.5rem 10vw;
}
.listings-title {
  width: 100%;
  text-align: center;
  margin: 0;
  padding: 0;
}
.loading {
  margin: 3rem;
}
</style>
