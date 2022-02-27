<script setup>
import TheWelcome from '@/components/TheWelcome.vue'
import rainImage from '../assets/rain.png'
</script>

<template>
  <div class="grow flex flex-row text-black h-full">
    <div class="w-full md:basis-3/4 bg-white pl-4">
      <span id="searchByCityText">Search by city</span>
      <span id="cityNameText" class="hidden"></span>
      <div class="pt-2 relative mx-auto text-gray-600">
        <input
          class="border-2 border-gray-300 bg-white h-10 px-5 pr-16 rounded-lg text-sm focus:outline-none"
          type="search"
          name="search"
          placeholder="Search"
        />
      </div>
      <br />

      <div class="grid grid-cols-1 md:grid-cols-2 justify-items-center">
        <!-- weather card -->
        <div
          class="relative h-64 w-11/12 md:w-9/12 flex items-end text-left bg-cover bg-center rounded-3xl border-2 border-gray-100 drop-shadow-lg"
          v-bind:style="{ 'background-image': 'url(' + rainImage + ')' }"
        >
          <div
            class="absolute top-0 right-0 left-0 mx-5 mt-2 flex justify-between items-center text-black"
          >
            <p class="px-1 py-2 font-semibold text-3xl">Sunny</p>
            <div class="font-regular flex flex-col justify-start">
              <span class="text-5xl leading-0 font-semibold">25° C</span>
            </div>
          </div>

          <div class="z-10 absolute bottom-0 right-0 left-0">
            <div class="mb-3 flex justify-evenly text-white text-center">
              <div class="bg-gray-600 rounded-2xl p-4 cursor-pointer group">
                <p class="text-sm py-1">Pressure</p>
                <p class="text-sm md:text-lg">400 bar</p>
              </div>
              <div class="bg-gray-600 rounded-2xl p-4 cursor-pointer group">
                <p class="text-sm py-1">Pressure</p>
                <p class="text-lg">400 bar</p>
              </div>
              <div class="bg-gray-600 rounded-2xl p-4 cursor-pointer group">
                <p class="text-sm py-1">Pressure</p>
                <p class="text-lg">400 bar</p>
              </div>
            </div>
          </div>
        </div>
        <!-- AQI Card -->
        <div
          class="relative h-64 w-11/12 md:w-9/12 flex items-end text-left bg-cover bg-center rounded-3xl border-2 border-gray-100 drop-shadow-lg"
          v-bind:style="{ 'background-image': 'url(' + rainImage + ')' }"
        >
          <div
            class="absolute top-0 right-0 left-0 mx-5 mt-2 flex justify-between items-center text-black"
          >
            <p class="px-1 py-2 font-semibold text-3xl">Air Quality</p>
            <div class="font-regular flex flex-col justify-start">
              <span class="text-5xl leading-0 font-semibold">390</span>
              <span class="text-sm text-right">PM 2.5</span>
            </div>
          </div>

          <div class="z-10 absolute bottom-0 right-0 left-0">
            <div class="mb-3 flex justify-evenly text-center">
              <div class="bg-white rounded-2xl p-4 cursor-pointer group w-10/12">
                <p class="text-xl py-1">Average</p>
              </div>
            </div>
          </div>
        </div>

      </div>
      <div class="py-10 px-4">
        <!-- hourly card -->
        <div
          class="relative h-80 w-full flex items-end text-left bg-cover bg-center rounded-xl border-2 border-gray-100 drop-shadow-xm"
        >
          <div
            class="absolute top-0 right-0 left-0 mx-5 mt-2 flex justify-between items-center text-black"
          >
            <p class="px-1 py-2 font-semibold text-3xl">How's the temperature today?</p>
            <div class="font-regular flex flex-col justify-start">
              <span class="text-xl leading-0 font-semibold">Tomorrow: 10/25 ° C</span>
            </div>
          </div>

          <div class="z-10 absolute bottom-0 right-0 left-0">
            <div class="flex justify-evenly text-white text-center">
              <div class="bg-gray-300 rounded-b-xl p-4 cursor-pointer group w-full h-40">
                <p class="text-sm py-1">Pressure</p>
                <p class="text-sm md:text-lg">400 bar</p>
              </div>
            </div>
          </div>
        </div>
       

      </div>

    </div>
    <div class="md:basis-1/4 bg-gray-100">
      <h3>To Do List</h3>
    </div>
  </div>
</template>
