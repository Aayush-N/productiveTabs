<script setup>
import { ref } from 'vue';
import axios from "axios";
import rainImage from '../assets/rain.png'
import cloudyImage from '../assets/cloudy.png'
import fewCloudsImage from '../assets/fewClouds.png'
import showerImage from '../assets/shower.png'
import snowImage from '../assets/snow.png'
import sunnyImage from '../assets/sunny.png'
import thunderstormImage from '../assets/thunderstorm.png'

import TodoSection from '../components/TodoSection.vue';
import QuotesCard from '@/components/QuotesCard.vue';
import FutureCard from '@/components/futureWeatherCard.vue';
import LoadingCard from '@/components/LoadingCard.vue'



let cityName = ref('');
cityName.value = 'Bangalore, India';

let todaysDate = new Date();

let hours = ref('');
let minutes = ref('');
let seconds = ref('');

function updateTime() {
  const date = new Date();
  hours.value = ('0'+date.getHours()).slice(-2);
  minutes.value = ('0'+date.getMinutes()).slice(-2);
  seconds.value = ('0'+date.getSeconds()).slice(-2); 
}
setInterval(() => { updateTime() }, 1000)

const currentWeather = ref('');
const tomorrowWeather = ref('');
const futureWeather = ref('');


function getWeather(lat, long) {
  const options = {
    method: 'GET',
    url: 'https://getweather.nandkeolyar.workers.dev/',
    params: {
      lat: lat,
      lon: long
    }
  };

  axios.request(options).then(function (response) {
    cityName.value = response.data.city.name + ', ' + response.data.city.country;
    currentWeather.value = response.data.list[0];
    tomorrowWeather.value = response.data.list[8];
    futureWeather.value = response.data.list.filter((element, index) => (index % 8 == 0 && index !== 0));
  }).catch(function (error) {
    console.error(error);
  });
}


function getLocation() {
  if (navigator.geolocation) {
    navigator.geolocation.getCurrentPosition(showPosition);
  } else {
    console.log("error")
  }
}

function showPosition(position) {
  getWeather(position.coords.latitude, position.coords.longitude);
}



getLocation();
</script>

<template>
  <div class="grow flex flex-col md:flex-row text-black h-full w-full">
    <div class="md:basis-3/4 bg-white">
      <div v-if="!currentWeather">
        <LoadingCard />
      </div>
      <div v-else>

      <div class="p-8 flex flex-col md:flex-row w-full justify-between">
        <div>
          <span id="cityNameText" class="text-3xl">{{ cityName }}</span>
        </div>

        <div class="text-gray-600 font-bold text-2xl">{{ hours }}:{{ minutes }}:{{ seconds }}</div>
      </div>

      <QuotesCard />

      <div class="grid grid-cols-1 md:grid-cols-3 justify-items-center">
        <!-- weather card -->
        <div
          class="relative h-64 w-10/12 flex items-end text-left bg-cover bg-center rounded-3xl border-2 border-gray-100 drop-shadow-md"
          v-bind:style="{ 'background-image': 'linear-gradient(rgb(255 255 255 / 40%), rgb(6 0 8 / 60%)), url(' + rainImage + ')' }"
        >
          <div
            class="absolute top-0 right-0 left-0 mx-5 mt-2 flex justify-between items-center text-black"
          >
            <p class="px-1 font-semibold text-3xl">{{ currentWeather.weather[0].main }}</p>
            <div class="font-regular flex flex-col justify-start">
              <span class="text-4xl leading-0 font-semibold">{{ currentWeather.main.temp }}°C</span>
              <span class="text-lg text-right">Feels like: {{ currentWeather.main.feels_like }}°C</span>
            </div>
          </div>

          <div class="z-10 absolute bottom-0 right-0 left-0">
            <div class="mb-3 flex justify-evenly text-white text-center">
              <div class="bg-orange-500 rounded-2xl p-3 cursor-pointer group">
                <p class="text-sm py-1">Pressure</p>
                <p class="text-sm md:text-lg">{{ currentWeather.main.pressure }} bar</p>
              </div>
              <div class="bg-lime-500 rounded-2xl p-3 cursor-pointer group">
                <p class="text-sm py-1">Humidity</p>
                <p class="text-sm md:text-lg">{{ currentWeather.main.humidity }}%</p>
              </div>
              <div class="bg-sky-500 rounded-2xl p-3 cursor-pointer group">
                <p class="text-sm py-1">Visibility</p>
                <p class="text-lg">{{ currentWeather.visibility }}m</p>
              </div>
            </div>
          </div>
        </div>
        <!-- Wind Card -->
        <div
          class="relative h-64 w-10/12 flex items-end text-left bg-cover bg-center rounded-3xl border-2 border-gray-100 drop-shadow-lg"
          v-bind:style="{ 'background-image': 'linear-gradient(rgb(255 255 255 / 40%), rgb(6 0 8 / 60%)), url(' + fewCloudsImage + ')' }"
        >
          <div
            class="absolute top-0 right-0 left-0 mx-5 mt-2 flex justify-between items-center text-black"
          >
            <p class="px-1 font-semibold text-3xl">Wind</p>
            <div class="font-regular flex flex-col justify-start">
              <span class="text-4xl leading-0 font-semibold">{{ currentWeather.wind.speed }} Km/h</span>
              <span class="text-lg text-right">Direction: {{ currentWeather.wind.deg }}°</span>
            </div>
          </div>

          <div class="z-10 absolute bottom-0 right-0 left-0">
            <div class="mb-3 flex justify-evenly text-center">
              <div class="bg-purple-200 rounded-xl p-4 cursor-pointer group w-10/12">
                <p class="text-xl py-1">Cloud Cover: {{ currentWeather.clouds.all }}%</p>
              </div>
            </div>
          </div>
        </div>
        <div
          class="relative h-64 w-10/12 flex items-end text-left bg-cover bg-center rounded-3xl border-2 border-gray-100 drop-shadow-lg"
          v-bind:style="{ 'background-image': 'linear-gradient(rgb(255 255 255 / 40%), rgb(6 0 8 / 60%)), url(' + sunnyImage + ')' }"
        >
          <div class="absolute top-0 right-0 left-0 mx-5 mt-2 flex justify-between text-black">
            <div class="font-regular flex flex-col justify-start">
              <p class="px-1 py-2 font-semibold text-3xl">Tomorrow</p>
              <p class="px-1 pt-2 font-semibold text-2xl">{{ tomorrowWeather.weather.main }}</p>
              <p class="px-1 font-semibold text-2xl">{{ tomorrowWeather.weather.description }}</p>
            </div>
            <div class="font-regular flex flex-col justify-start">
              <span class="text-3xl py-2 leading-0 font-semibold">{{ tomorrowWeather.main.temp }}°C</span>
              <span class="text-lg text-right">Feels like: {{ tomorrowWeather.main.feels_like }}°C</span>
            </div>
          </div>
        </div>
      </div>

      <div class="py-10 px-8">
        <!-- future card -->
        <div
          class="h-auto text-left bg-cover bg-center rounded-xl border-2 border-gray-100 drop-shadow-xm"
        >
          <div class="mx-5 mt-2 flex flex-col md:flex-row justify-between items-center text-black">
            <p class="px-1 py-2 font-semibold text-3xl">The week ahead</p>
          </div>
          <div class="flex flex-col md:flex-row gap-4 p-4 mb-6 w-full justify-between items-center">
            <span v-for="(weather, index) in futureWeather">
              <FutureCard
                :imageURL="'http://openweathermap.org/img/wn/' + weather.weather[0].icon + '@2x.png'"
                :date="weather.dt"
                :temp="weather.main.temp"
                :feels_like="weather.main.feels_like"
              />
            </span>
          </div>
        </div>
      </div>
    </div>
    </div>

    <div class="md:basis-1/4 bg-gray-100">
      <TodoSection />
    </div>
  </div>
</template>
