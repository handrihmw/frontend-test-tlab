<template>
  <div class="flex justify-between items-center max-w-screen-xl mx-auto">
    <div>
      <h2 class="text-slate-100 text-md">Daftar Game</h2>
    </div>
    <div>
      <label for="filter" class="block mb-2 text-sm font-medium sr-only text-gray-900 dark:text-white"
        >Select an option</label
      >
      <select
        id="filter"
        class="bg-gray-50 text-gray-900 text-sm focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
      >
        <option selected>Semua Genre</option>
        <option value="all">Semua Genre</option>
        <option value="title">Judul</option>
        <option value="platform">Platform</option>
      </select>
    </div>
  </div>
</template>
