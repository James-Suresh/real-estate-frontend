<template>
    <div class="real-estate-card">
        <img :src="image" alt="Real Estate Image" class="card-image" />
        <div class="card-details">
          <div class="price">{{ price }}</div>
          <div class="address">{{ address }}</div>
        </div>
      </div>
    </template>
    
    <script>
    import { defineProps } from 'vue';
    
    export default {
      props: {
        image: String,
        price: String,
        address: String,
      },
    };
    </script>
    
    <style scoped>
    .real-estate-card {
      display: flex;
      margin: 0;
      flex-direction: column;
      width: 300px;
      background-color: #ffffff;
      border: 1px solid #e0e0e0;
      border-radius: 4px;
      padding: 10px;
      box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
      
      
    }

    a:hover{

    }
    
    .card-image {
      width: 100%;
      height: auto;
      margin-bottom: 10px;
    }
    
    .card-details {
      flex: 1;
    }
    
    .price {
      font-size: 18px;
      font-weight: bold;
      margin-bottom: 5px;
    }
    
    .address {
      font-size: 14px;
      color: #666666;
    }
    </style>