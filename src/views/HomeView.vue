<script setup>
  import carsData from "../data.json"
  import { ref, computed, onMounted } from 'vue';
  import { useRouter, useRoute } from 'vue-router';

  const router = useRouter()
  const route = useRoute()
  const cars = ref(carsData)
  const name = ref("all")

  onMounted(() => {
    name.value = route.query.name || "all"
  })

  const filteredCars = computed(() => {
    if (name.value !== "all") {
      return cars.value.filter(c => c.name.toLowerCase() === name.value)
    }
    return cars.value
  })

  const handleChange = () => {
    router.push({ query: { name: name.value } })
  }

</script>

<template>
  <div class="container">
    <h1 class="heading">Our Cars</h1>
    <select @change="handleChange" v-model="name">
      <option value="all">All</option>
      <option value="ferrari">Ferrari</option>
      <option value="bmw">BMW</option>
      <option value="nissan">Nissan</option>
      <option value="bentley">Bentley</option>
      <option value="porsche">Porsche</option>
    </select>
    <div class="cards">
      <div v-if="filteredCars.length !== 0" @click="router.push(`/car/${car.id}`)" class="card"
        v-for="car in filteredCars" :key="car.make">
        <p class="name">{{ car.name }} {{ car.make }}</p>
        <p class="price">${{ car.price }}</p>
      </div>
      <div v-else>
        <p>No data found :(</p>
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
    width: 280px;
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
