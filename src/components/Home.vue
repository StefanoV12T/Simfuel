<script setup>
import { defineProps, defineEmits } from 'vue';

// Definisci le props se necessario
// const props = defineProps(['...']);


//mi permette di richiamare al componente padre una funzione con un determinato valore che paserò con un evento 
const emit = defineEmits(['changeTab']);

</script>

<template>
    <div class="hero">
  <div class="hero-content flex-col lg:flex-row">
    <img
      src="../images/fuel.png"
      class="max-w-sm mask mask-squircle rounded-lg shadow-2xl" />
    <div>
      <h1 class="text-5xl font-bold">SimFuel</h1>
      <p class="py-6">
        Questa è un'app che ti permette di imbarcare il quantitativo giusto di carburante nel serbatoio, in base alle tue esigenze!
      </p>
      <!-- qui richiamo la funzione da passare al componente padre e il valore che cambia -->
      <button class="btn btn-secondary" @click="emit('changeTab', 2);">Accedi al calcolatore</button>
    </div>
  </div>
</div>
</template>