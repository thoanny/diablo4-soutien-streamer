<script setup>
import { ref } from 'vue';
import streamers from './streamers.json';

const currentStreamers = ref(streamers);
const filter = ref(null);

function handleFilter() {
  if (filter.value.length <= 0) {
    currentStreamers.value = streamers;
  } else {
    currentStreamers.value = streamers.filter((s) => {
      return s['login'].includes(filter.value);
    });
  }
}

</script>

<template>
  <header class="overflow-hidden relative mb-6">
    <img src="@/assets/banner.png" class="h-full w-full object-cover absolute top-0 left-0 z-10 opacity-30" alt="">
    <div class="relative h-full w-full flex flex-col gap-4 items-center justify-center z-20">
      <img src="@/assets/logo.png" alt="">
      <h1 class="text-white text-4xl font-semibold max-w-3xl text-center">
        PROGRAMME DE SOUTIEN À UN STREAMER OU À UNE STREAMEUSE
      </h1>
    </div>
  </header>

  <main class="container mx-auto px-4">
    <input type="text" class="input input-lg input-bordered w-full mb-6"
      placeholder="Chercher un streamer ou une streameuse" v-model="filter" @keyup="handleFilter">
    <div v-if="currentStreamers.length === 0" class="text-lg">Aucune streameuse ou streamer trouvé...</div>
    <ul class="grid grid-cols-5 gap-4">
      <li v-for="streamer in currentStreamers">
        <a :href="streamer.url" target="_blank" rel="noreferrer"
          class="btn btn-primary btn-lg btn-block justify-between font-semibold flex-nowrap">
          <div class="truncate">{{ streamer.login }}</div>
          <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor" class="w-5 h-5 flex-shrink-0">
            <path fill-rule="evenodd"
              d="M4.25 5.5a.75.75 0 00-.75.75v8.5c0 .414.336.75.75.75h8.5a.75.75 0 00.75-.75v-4a.75.75 0 011.5 0v4A2.25 2.25 0 0112.75 17h-8.5A2.25 2.25 0 012 14.75v-8.5A2.25 2.25 0 014.25 4h5a.75.75 0 010 1.5h-5z"
              clip-rule="evenodd" />
            <path fill-rule="evenodd"
              d="M6.194 12.753a.75.75 0 001.06.053L16.5 4.44v2.81a.75.75 0 001.5 0v-4.5a.75.75 0 00-.75-.75h-4.5a.75.75 0 000 1.5h2.553l-9.056 8.194a.75.75 0 00-.053 1.06z"
              clip-rule="evenodd" />
          </svg>
        </a>
      </li>
    </ul>
  </main>

  <footer class="container mx-auto px-4 text-center my-6 opacity-75">
    Fait avec ❤ et peu de temps par <a href="https://thoanny.fr" target="_blank" class="underline">Thoanny</a>
  </footer>
</template>

<style scoped>
header {
  height: 75vh;
}
</style>
