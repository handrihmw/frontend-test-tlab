<template>
  <div class="flex justify-between items-center max-w-screen-xl mx-auto">
    <div class="mb-5">
      <h2 class="text-slate-100 text-md hidden md:block">Daftar Game</h2>
    </div>
    <div class="mb-5">
      <label
        for="filter"
        class="block mb-2 text-sm font-medium sr-only text-gray-900 dark:text-white"
        >Select an option</label
      >
      <select
        id="filter"
        v-model="selectedOption"
        @change="filterData"
        class="bg-gray-50 text-gray-600 rounded w-48 text-sm focus:ring-blue-500 focus:border-blue-500 block p-2.5"
      >
        <option value="all">Semua Genre</option>
        <option value="alphabet">Urutkan A-Z</option>
        <option value="browser">Web Browser</option>
        <option value="pc">PC (Windows)</option>
        <option value="shooter">Shooter</option>
        <option value="mmorpg">Mmorpg</option>
        <option value="release">Release Date</option>
      </select>
    </div>
  </div>
  <div
    class="mx-auto mb-10 grid gap-6 max-w-screen-xl grid-cols-1 md:grid-cols-2 lg:grid-cols-3 xl:grid-cols-3 justify-center"
  >
    <article
      v-for="(item, index) in items"
      :key="index"
      class="group p-3 pb-4 overflow-hidden bg-white shadow-md rounded-lg hover:bg-white hover:shadow-lg lg:mb-0"
    >
      <img class="w-full rounded" :src="item.thumbnail" :alt="item.title" />
      <span
        class="inline-block relative bottom-10 left-3 bg-blue-100 rounded-full px-3 py-1 text-sm font-semibold text-blue-900"
        >{{ item.genre }}</span
      >
      <div class="p-2 pt-0">
        <h3 class="text-xl mb-2">{{ item.title }}</h3>
        <p class="text-gray-700 text-base line-clamp-2 text-ellipsis">
          {{ item.short_description }}
        </p>
      </div>
      <hr class="my-2" />
      <div class="p-2 flex justify-between mt-3 text-start">
        <div class="flex-1 flex-col gap-1">
          <p class="text-xs text-gray-400 font-light">Platform</p>
          <p class="text-md text-gray-700">{{ item.platform }}</p>
        </div>
        <div class="flex-1 flex-col gap-1">
          <p class="text-xs text-gray-400 font-light">Release Date</p>
          <p class="text-md text-gray-700">{{ item.release_date }}</p>
        </div>
      </div>
    </article>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'

interface Game {
  title: string
  short_description: string
  thumbnail: string
  platform: string
  release_date: string
  category: string
  genre: string
}

const items = ref<Game[]>([])
const selectedOption = ref<string>('all')

async function fetchGames(query: string = '') {
  try {
    const endpoint = `https://free-to-play-games-database.p.rapidapi.com/api/games${query}`
    const config = {
      headers: {
        'Content-Type': 'application/json',
        'X-RapidAPI-Key': '6ca948ceb7msh426f11ced47c1b7p13741cjsnf6f65942f5df',
        'X-RapidAPI-Host': 'free-to-play-games-database.p.rapidapi.com'
      }
    }
    const response = await fetch(endpoint, config)
    const res_json = await response.json()
    items.value = res_json as Game[]
    // console.info(items.value)
  } catch (error) {
    // console.error('Error occurred:', error)
  }
}

const queryMapping: Record<string, string> = {
  all: '',
  alphabet: '?sort-by=alphabetical',
  browser: '?platform=browser',
  pc: '?platform=pc',
  shooter: '?category=shooter',
  mmorpg: '?category=mmorpg',
  release: '?sort-by=release-date'
}

function filterData() {
  const selectedQuery = queryMapping[selectedOption.value]

  fetchGames(selectedQuery)
}

onMounted(() => fetchGames())
</script>
