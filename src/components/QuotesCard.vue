<script setup>
import { ref } from 'vue';
import axios from "axios";
const quoteText = ref('');
const quoteAuthor = ref('');
const options = {method: 'GET', url: 'https://api.quotable.io/random'};

axios.request(options).then(function (response) {
  quoteText.value = response.data.content;
  quoteAuthor.value = response.data.author;
}).catch(function (error) {
  console.error(error);
});
</script>
<template>
	<div class="grid grid-cols-6 m-8 rounded-xl bg-blue-800">
        <div class="col-span-4">
          <h2 class="font-bold text-3xl text-white ml-10 mt-8">{{quoteText}}</h2>
          <p class="font-light text-white text-sm ml-10 my-5">{{quoteAuthor}}</p>
        </div>

        <div class="col-span-2 relative">
          <img src="https://www.digitalocean.com/_next/static/media/cloudJourneyImage.954519ea.svg" />
        </div>
      </div>
</template>