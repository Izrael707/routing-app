<script setup>

  import { useRoute } from 'vue-router';
  import { ref, onBeforeMount } from 'vue';
  import cars from "../data.json"

  const car = ref(null)
  const route = useRoute()
  const { id } = route.params
  onBeforeMount(() => {
    car.value = cars.find(c => c.id === parseInt(id))
  })

</script>

<template>
  <div class="container">
    <div v-if="car" class="card">
      <h1 class="heading">The Car</h1>
      <p class="make">Make: {{ car.make }}</p>
      <p class="name">Name: {{ car.name }}</p>
      <p class="price">Price: ${{ car.price }}</p>
    </div>
    <div v-else>
      <h1 class="heading">Car not Found :(</h1>
    </div>
  </div>
</template>

<style scoped>
  .card {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 12px;
  }

  .make,
  .name,
  .price {
    font-size: 20px;
    font-style: oblique;
    border: 1px solid #eee;
    padding: 12px;
  }
</style>