<script setup>
import axios from 'axios';
import { onMounted, ref, computed } from 'vue';

let lapTimeMinutes =ref('');
let lapTimeSeconds=ref('');
let lapTimeMilliseconds = ref('');
let lapTime = ref('');



let raceTimeHours=ref('');
let raceTimeMinutes = ref('');
let raceTime = ref('');

let consumoCarburante=ref('');
let iniettaCarburante=ref(0);
let error = ref(0);


function cacca(num) {
    console.log(num);
}

function CalcolaBenzina() {
    if(lapTimeSeconds.value=='') {
        lapTimeSeconds.value = 0; 
    };
    if (lapTimeMinutes.value=='') {
        lapTimeMinutes.value = 0; 
        console.log('maledetto bastardo');
    };
    if (lapTimeMilliseconds.value =='') {
        lapTimeMilliseconds.value = 0; 
    };
    if (raceTimeHours.value == '') {
        raceTimeHours.value = 0; 
    };
    if (raceTimeMinutes.value == '') {
        raceTimeMinutes.value = 0; 
    };
    console.log(typeof parseInt(lapTimeMilliseconds.value));
    lapTime.value =(parseInt(lapTimeMinutes.value) * 60000) +( parseInt(lapTimeSeconds.value) * 1000) + parseInt(lapTimeMilliseconds.value);
    console.log('il tempo è di '+ lapTime.value);
    raceTime.value = parseInt(raceTimeHours.value * 3600000) + parseInt(raceTimeMinutes.value * 60000);
    console.log(raceTime.value);
    error.value = 0;
    if (raceTime.value <= 0 || lapTime.value <= 0 || consumoCarburante.value <= 0) {
        console.log(error);
        return error.value = 1;
    }
    iniettaCarburante.value =((raceTime.value) / lapTime.value) * consumoCarburante.value;
}


</script>

<template>
    <div v-if="error==1" role="alert" class="alert alert-error">
        <svg
            xmlns="http://www.w3.org/2000/svg"
            class="h-6 w-6 shrink-0 stroke-current"
            fill="none"
            viewBox="0 0 24 24">
            <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M10 14l2-2m0 0l2-2m-2 2l-2-2m2 2l2 2m7-2a9 9 0 11-18 0 9 9 0 0118 0z" />
        </svg>
        <span>Errore, controlla i dati inseriti</span>
    </div>

  <!-- Dati del giro -->
<span class="label label-text  md:w-2/5 mx-auto">Inserisci qui il tuo tempo sul giro</span>

<div class="flex flex-row md:w-2/5 mx-auto">
      
    <div class="basis-1/3 mr-2">
    <input type="number" v-model="lapTimeMinutes" placeholder="mm" class="input input-bordered input-primary w-full max-w-xs" />
    </div>

    <div class="basis-1/3 mr-2">
    <input type="number"  v-model="lapTimeSeconds" placeholder="ss" class="input input-bordered input-primary w-full max-w-xs" />
    </div>

    <div class="basis-1/3">
    <input type="number" placeholder="ms" v-model="lapTimeMilliseconds" class="input input-bordered input-primary w-full max-w-xs" />
    </div>
    
</div>
  
<span class="label label-text mt-5  md:w-2/5 mx-auto">Inseriscila durata della gara</span>

<div class="flex flex-row mx-auto md:w-2/5 w-full">
      
    <div class="basis-1/2 w-full mr-2">
    <input type="number" v-model="raceTimeHours" placeholder="hh" class="input input-bordered input-primary w-full  m-0" />
    </div>

    <div class="basis-1/2 w-full">
    <input type="number" v-model="raceTimeMinutes" placeholder="mm" class="input input-bordered input-primary w-full m-0" />
    </div>
    
</div>

   
<span class="label label-text mt-5  md:w-2/5 mx-auto">Inserisci il consumo di carburante per giro</span>
    <div class="w-full md:w-2/5 mx-auto ">
    <label class="input input-bordered  input-primary flex items-center gap-2">
        <input v-model="consumoCarburante"  type="number" class="grow" placeholder="L"/>
        <!-- <kbd @click="addProductFromIcon(productInput)" class="kbd kbd-sm">Enter</kbd> -->
    </label>
    </div>

    <div class="w-full md:w-2/5 mx-auto mt-10">
        <h1 @click="CalcolaBenzina" class="btn btn-secondary mb-2">Calcola carburante da inserire</h1>
    <label class="input input-bordered flex items-center gap-2">
      
        <span class="grow">
            {{ iniettaCarburante }} L
        </span>
        <!-- <kbd @click="addProductFromIcon(productInput)" class="kbd kbd-sm">Enter</kbd> -->
    </label>
    </div>

 



</template>