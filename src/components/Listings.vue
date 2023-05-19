<script setup>
import axios from 'axios'
import { ref,watch, computed } from 'vue'
import Card from './Card.vue'
import Loading from './Loading.vue'
import Hero from './Hero.vue';

const houses = ref(0)
const props = defineProps({
  loc: Object
})

const isFetching = ref(true);

const list_loc = ref(props.loc);



const options = ref({
  method: 'GET',
  url: 'https://realty-in-ca1.p.rapidapi.com/properties/list-residential',
  params: {
    
    LatitudeMax:list_loc.value.latMax,
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
const fetchProperties = async () => {
  try {
    isFetching.value = true
    const response = await axios.request(options.value)
    console.log(response.data)
    houses.value = response.data.Results.map((result) => ({
      price: result.Property.Price,
      address: result.Property.Address?.AddressText.split("|")[0],
      image: result.Property.Photo[0]?.MedResPath
    }))
    isFetching.value = false
  } catch (error) {
    console.error(error)
  }
}
//fetchProperties()

watch(list_loc.value, (newValue, oldValue) => {

  console.log("change")
  options.value = {
  method: 'GET',
  url: 'https://realty-in-ca1.p.rapidapi.com/properties/list-residential',
  params: {
    
    LatitudeMax:list_loc.value.latMax,
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
}

 fetchProperties();
});


fetchProperties()
</script>

<template>
  <div class="listings">
    <h1 class="listings-title">Listings</h1>



    <Loading v-if="isFetching"/>

    <div v-else v-for= "house,index in houses" :key="index" :house="house" :style="{ transitionDelay: `${index * 100}ms` }">
      <transition-group name="fade" tag="div">
      <Card 
    
    :image="house.image"
    :price="house.price"
    :address="house.address"
    />
  </transition-group>
    </div>

    


    </div>
</template>
<style scoped>
.listings {
  width: 100vw;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 2rem;
  padding: 2rem 10vw;
}
.listings-title {
  width: 100%;
  text-align: center;
}
</style>
