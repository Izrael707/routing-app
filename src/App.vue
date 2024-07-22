<script setup>
  import { RouterView, RouterLink } from 'vue-router';
</script>

<template>
  <main>
    <div class="links">
      <RouterLink active-class="active" to="/">Home</RouterLink>
      <RouterLink active-class="active" to="/about">About</RouterLink>
    </div>
    <RouterView />
  </main>
</template>

<style scoped>
  .links {
    padding: 16px;
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    display: flex;
    gap: 20px;
    border-bottom: 1px solid #ddd;
  }

  .links .active {
    font-weight: 500;
  }

  .links a {
    text-decoration: none;
    font-size: 20px;
    color: #333;
    transition: color 0.25s;
  }

  .links a:hover {
    color: gray;
  }
</style>