<template>
  <div class="bg-slate-100">
    <Navbar />
    <Header />
    <div class="px-3 md:px-10 py-6 md:py-16 flyout">
      <Card />
    </div>
  </div>
</template>

<script setup lang="ts">
import Navbar from './components/Navbar.vue'
import Header from './components/Header.vue'
import Card from './components/Card.vue'
</script>

<style lang="scss" scoped>
  .flyout {
    position: relative;
    top: 0;

    @media (min-width: 767.98px) {
      top: -200px;
    }
  }
</style>