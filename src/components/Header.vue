<template>
  <div class="w-100 header p-10">
    <Hero />
    <Filter />
  </div>
</template>

<script setup lang="ts">
import Hero from './Hero.vue'
import Filter from './Filter.vue'
</script>

<style lang="scss" scoped>
.header {
  background-color: #1F7CD1;
  height: 400px;
}
</style>