<script setup>
import { ref, onMounted } from 'vue';
import Tabs from './components/Tabs.vue';

const themes = [
  { label: 'Light', value: 'light' },
  { label: 'Dark', value: 'dark' },
  { label: 'Cupcake', value: 'cupcake' },
  { label: 'Bumblebee', value: 'bumblebee' },
  { label: 'Emerald', value: 'emerald' },
  { label: 'Corporate', value: 'corporate' },
  { label: 'Synthwave', value: 'synthwave' },
  { label: 'Retro', value: 'retro' },
  { label: 'Cyberpunk', value: 'cyberpunk' },
  { label: 'Valentine', value: 'valentine' },
  { label: 'Halloween', value: 'halloween' },
  { label: 'Garden', value: 'garden' },
  { label: 'Forest', value: 'forest' },
  { label: 'Aqua', value: 'aqua' },
  { label: 'Lofi', value: 'lofi' },
  { label: 'Pastel', value: 'pastel' },
  { label: 'Fantasy', value: 'fantasy' },
  { label: 'Wireframe', value: 'wireframe' },
  { label: 'Black', value: 'black' },
  { label: 'Luxury', value: 'luxury' },
  { label: 'Dracula', value: 'dracula' },
  { label: 'CMYK', value: 'cmyk' },
  { label: 'Autumn', value: 'autumn' },
  { label: 'Business', value: 'business' },
  { label: 'Acid', value: 'acid' },
  { label: 'Lemonade', value: 'lemonade' },
  { label: 'Night', value: 'night' },
  { label: 'Coffee', value: 'coffee' },
  { label: 'Winter', value: 'winter' },
  { label: 'Dim', value: 'dim' },
  { label: 'Nord', value: 'nord' },
  { label: 'Sunset', value: 'sunset' },
];


const currentTheme = ref('default');

onMounted(() => {
  // Carica il tema salvato dal localStorage
  const savedTheme = localStorage.getItem('theme');
  if (savedTheme) {
    currentTheme.value = savedTheme;
  }
});

const setTheme = (theme) => {
  currentTheme.value = theme;
  // Salva il tema selezionato nel localStorage
  localStorage.setItem('theme', theme);
};
</script>

<template>
  <!-- scelta Tema -->
  <div :class="currentTheme">
    <div class="dropdown">
      <div tabindex="0" role="button" class="btn m-1">
        Tema
        <svg
          width="12px"
          height="12px"
          class="inline-block h-2 w-2 fill-current opacity-60"
          xmlns="http://www.w3.org/2000/svg"
          viewBox="0 0 2048 2048">
          <path d="M1799 349l242 241-1017 1017L7 590l242-241 775 775 775-775z"></path>
        </svg>
      </div>
      <ul tabindex="0" class="dropdown-content bg-base-300 rounded-box z-[1] w-52 p-2 shadow-2xl max-h-60 overflow-y-auto">
        <li v-for="theme in themes" :key="theme.value">
          <input
            type="radio"
            name="theme-dropdown"
            class="theme-controller btn btn-sm btn-block btn-ghost justify-start"
            :aria-label="theme.label"
            :value="theme.value"
            @change="setTheme(theme.value)"
            :checked="currentTheme === theme.value"
          />
        </li>
      </ul>
    </div>
  </div>
  <!-- contenuto -->
  <div class="w-full">
    <div class="flex justify-center pb-3">
      <h1 class="text-5xl font-bold underline">SimFuel</h1>            
    </div>
  </div>

  <Tabs />
</template>

<style scoped>

</style>
