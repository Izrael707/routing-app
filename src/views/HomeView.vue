<script setup>
  import carsData from "../data.json"
  import { ref } from 'vue';
  import { useRouter } from 'vue-router';

  const router = useRouter()
  const cars = ref(carsData)
</script>

<template>
  <div class="container">
    <h1 class="heading">Our Cars</h1>
    <div class="cards">
      <div @click="router.push(`/car/${car.id}`)" class="card" v-for="car in cars" :key="car.make">
        <p class="name">{{ car.name }} {{ car.make }}</p>
        <p class="price">${{ car.price }}</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
  .cards {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 24px;
  }

  .card {
    padding: 24px;
    box-shadow: 4px 4px 8px rgba(0, 0, 0, 0.1);
    border-radius: 4px;
    width: 240px;
    text-wrap: balance;
    transition: transform 0.25s;
    cursor: pointer;
  }

  .card:hover {
    transform: scale(1.1)
  }

  .card:active {
    transform: none
  }

  .name {
    font-size: 24px;
    font-weight: 500;
  }

  .price {
    font-size: 16px;
  }
</style>
