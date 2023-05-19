
<script setup>
import axios from 'axios'
    import { processExpression } from "@vue/compiler-core";
    import {ref} from "vue"
import Card from "./Card.vue"
import Loading from "./Loading.vue"


const houses = ref(0);
const options = {
  method: 'GET',
  url: 'https://realty-in-ca1.p.rapidapi.com/properties/list-residential',
  params: {
    LatitudeMax: '81.14747595814636',
    LatitudeMin: '-22.26872153207163',
    LongitudeMax: '-10.267941690981388',
    LongitudeMin: '-136.83037765324116',
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
      };

     

const fetchProperties = async () => {
      try {
        const response = await axios.request(options);
        console.log(response.data)
        houses.value = response.data.Results.map((result)=>({
          price: result.Property.Price,
          address: result.Property.Address?.AddressText,
          image: result.Property.Photo[0]?.MedResPath
        }))
      } catch (error) {
        console.error(error);
      }
    };
   //fetchProperties()

</script>

<template>
    <div class="listings">

        <h1 class="listings-title">Listings</h1>
        
<!-- 
        <div v-for="house in houses" :key="house.id" :house="house">

          <Card
        :image="house.image"
        :price="house.price"
        :address="house.address"
        />
        </div> -->

        <Card
        class="animate__animated animate__fadeInUp animate__delay-2s"
        image="src\assets\real-estate-bg.jpg"
        price="house.price"
        address="house.address"
        />
        <Loading/>
        
       
    </div>
</template>
<style scoped>
    .listings{
      background-color: rgba(0,0,0, 0.05);
      
        width: 100vw;
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
        gap: 1rem;
        padding: 2rem 10vw;
    }
    .listings-title{
        width: 100%;
        text-align: center;
    }
</style>