<script setup>
import { ref } from 'vue';
import Home from './Home.vue';
import SimFuel from './SimFuel.vue';
let tab = ref(1);

// Funzione per gestire il cambio di tab
function handleChangeTab(newTab) {
  tab.value = newTab;
}

</script>

<template>

  <div class="w-full">
    <div class="flex justify-center px-5 pt-3">
      <button class="btn btn-xs mr-5 sm:btn-sm md:btn-md lg:btn-lg" @click="tab=1" :class="{ 'btn-neutral' : tab === 1}">Home</button>
      <button class="btn btn-xs sm:btn-sm md:btn-md lg:btn-lg"  @click="tab=2" :class="{ 'btn-neutral' : tab === 2}">SimFuel</button>
    </div>
      <!-- Contenuto -->
    <div>
      <!--ascolto la funzione changeTab in Home, e avvio la funzione hangleChangeTab qui in tabs  -->
      <div v-if="tab===1" class="px-10"> <Home @changeTab="handleChangeTab" />
      </div>
      <div v-if="tab===2" class="py-10 px-6"><SimFuel /></div>
    </div>
  </div>

</template>