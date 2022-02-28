<script setup>
import { defineProps} from "vue";
const props = defineProps({
  imageURL: String,
  date: Number,
  temp: Number,
  feels_like: Number,
})

let weatherDate = new Date(0)
weatherDate.setUTCSeconds(props.date)
const formattedDate = weatherDate.toLocaleDateString('en-GB', {
  day: 'numeric', month: 'short', year: 'numeric'
}).replace(/ /g, ' ');
</script>

<template>
	<div
		class="p-4 w-80 bg-white flex items-center rounded-lg shadow-md hover:scale-105 transition transform duration-500 cursor-pointer border"
	>
		<div>
			<img :src="imageURL" alt="weather icon">
		</div>
		<div>
			<h1 class="text-xl font-bold text-gray-700 mb-2">{{formattedDate}}</h1>
			<p class="text-gray-600 text-sm">Temperature: {{temp}}°C</p>
			<p class="text-gray-600 text-sm">Feels Like: {{feels_like}}°C</p>
		</div>
	</div>
</template>
