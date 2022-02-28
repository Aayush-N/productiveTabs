<script setup>
import { ref } from 'vue';

</script>
<template>
	<div class="grid grid-cols-6 m-8 rounded-xl bg-blue-800">
        <div class="col-span-4">
          <h2 class="font-bold text-3xl text-white ml-10 mt-8">Loading....</h2>
		  <p class="font-light text-white text-sm ml-10 my-5">Please provide access to your current location</p>
        </div>

        <div class="col-span-2 relative">
          <img src="https://www.digitalocean.com/_next/static/media/cloudJourneyImage.954519ea.svg" />
        </div>
      </div>
</template>