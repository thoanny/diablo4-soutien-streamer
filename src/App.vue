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
    <ul class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 xl:grid-cols-5 gap-4">
      <li v-for="streamer in currentStreamers.slice(0, 100)">
        <a :href="streamer.url" target="_blank" rel="noreferrer"
          class="btn btn-primary btn-lg btn-block font-semibold flex-nowrap">
          <div class="truncate">{{ streamer.login }}</div>
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
