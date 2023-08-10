<template>
  <div class="w-100 header p-5 md:p-10">
    <Hero />
  </div>
</template>

<script setup lang="ts">
import Hero from './Hero.vue'
</script>

<style lang="scss" scoped>
.header {
  background-color: #1f7cd1;
  height: 300px;

  @media screen and (min-width: 768px) {
    height: 400px;
  }
}
</style>
