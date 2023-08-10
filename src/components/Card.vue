<template>
  <div class="mx-auto mb-10 grid max-w-screen-xl grid-cols-1 px-0 md:grid-cols-3 xl:grid-cols-3 xl:px-1 justify-center">
    <article v-for="(item, index) in items" :key="index" class="group p-3 pb-4 m-2 overflow-hidden bg-white shadow-md dark:bg-cyan-900/50 rounded-lg hover:bg-white hover:shadow-lg lg:mb-0">
      <img class="w-full rounded" :src="item.thumbnail" :alt="item.title">
      <div class="p-2 mt-3">
        <h3 class="text-xl mb-2">{{ item.title }}</h3>
        <p class="text-gray-700 text-base line-clamp-2 text-ellipsis">{{ item.short_description }}</p>
      </div>
      <hr class="my-2">
      <div class="p-2 flex justify-between mt-3 text-start">
        <div class="flex flex-col gap-1">
          <p class="text-xs text-gray-400 font-light">Platform</p>
          <p class="text-md text-gray-700">{{ item.platform }}</p>
        </div>
        <div class="flex flex-col gap-1">
          <p class="text-xs text-gray-400 font-light">Release Date</p>
          <p class="text-md text-gray-700">{{ item.release_date }}</p>
        </div>
      </div>
    </article>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue';

interface Game {
  title: string;
  short_description: string;
  thumbnail: string;
  platform: string;
  release_date: string;
}

const items = ref<Game[]>([]);

async function getData() {
  try {
    const config = {
      headers: {
        "Content-Type": "application/json",
        "X-RapidAPI-Key": '6ca948ceb7msh426f11ced47c1b7p13741cjsnf6f65942f5df',
        "X-RapidAPI-Host": 'free-to-play-games-database.p.rapidapi.com',
      },
    };
    const response = await fetch('https://free-to-play-games-database.p.rapidapi.com/api/games', config);
    const res_json = await response.json();
    items.value = res_json as Game[];
  } catch (error) {
    console.log("Error occurred:", error);
  }
}

onMounted(getData);
</script>
