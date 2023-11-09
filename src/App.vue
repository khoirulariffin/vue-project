<template>
  <nav class="w-full flex justify-center items-center mt-10">
    <ul class="flex flex-row gap-10">
      <RouterLink to="/">Home</RouterLink>
      <RouterLink to="/about">About</RouterLink>
    </ul>
  </nav>
  <RouterView />
</template>

<script setup>
import { RouterView, RouterLink } from 'vue-router'
</script>
