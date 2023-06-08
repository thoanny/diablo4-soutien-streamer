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
      return s['login'].toLowerCase().includes(filter.value.replace(/\s+/g, '').toLowerCase());
    });
  }
}

</script>

<template>
  <header class="overflow-hidden relative mb-6 px-4">
    <img src="@/assets/banner.png" class="h-full w-full object-cover absolute top-0 left-0 z-10 opacity-30" alt="">
    <div class="relative h-full w-full flex flex-col gap-4 items-center justify-center z-20">
      <img src="@/assets/logo.png" alt="">
      <h1 class="text-white text-4xl font-semibold max-w-3xl text-center">
        PROGRAMME DE SOUTIEN À UN STREAMER OU À UNE STREAMEUSE
      </h1>
      <a href="https://news.blizzard.com/fr-fr/diablo4/23954936/drops-twitch-pour-le-lancement-de-diablo-iv-obtenez-la-monture-instinct-primal"
        target="_blank" rel="noreferrer" class="btn btn-primary">Plus d'infos</a>
    </div>
  </header>

  <main class="container mx-auto px-4">
    <p class="text-center">La limite d'affichage est définie à 100 pour des raisons de performance (il y a <a
        href="https://bnetcmsus-a.akamaihd.net/cms/page_media/20/20E7LR2225OK1685047410111.pdf" target="_blank"
        rel="noreferrer" class="underline">{{
          streamers.length }} personnes</a> dans le programme).</p>
    <p class="text-center mb-6 font-semibold">Utilisez le champ de recherche ci-dessous pour savoir si vos streameuses et
      streamers
      préférés font partie de ce
      programme.</p>
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
