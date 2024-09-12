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
let iniettaCarburante = ref(0);
let iniettaCarburanteSafe = ref(0);
let iniettaCarburanteLapPlus = ref(0);
let error = ref(0);


function CalcolaBenzina() {
    if(lapTimeSeconds.value=='') {
        lapTimeSeconds.value = 0; 
    };
    if (lapTimeMinutes.value=='') {
        lapTimeMinutes.value = 0; 
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
    
    lapTime.value =(parseInt(lapTimeMinutes.value) * 60000) +( parseInt(lapTimeSeconds.value) * 1000) + parseInt(lapTimeMilliseconds.value);
    
    raceTime.value = parseInt(raceTimeHours.value * 3600000) + parseInt(raceTimeMinutes.value * 60000);
    
    error.value = 0;
    if (raceTime.value <= 0 || lapTime.value <= 0 || consumoCarburante.value <= 0) {
        return error.value = 1;
    }

    iniettaCarburante.value = Math.floor((((raceTime.value) / lapTime.value)+1) * consumoCarburante.value) + 2;
    iniettaCarburanteSafe.value = iniettaCarburante.value +3;
    iniettaCarburanteLapPlus.value =  Math.floor(iniettaCarburante.value + consumoCarburante.value)+1;
}

function ResettaDati(){
    lapTimeSeconds.value = '';
    lapTimeMinutes.value = '';
    lapTimeMilliseconds.value = '';
    raceTimeHours.value = '';
    raceTimeMinutes.value = '';
    iniettaCarburante.value = 0;
    iniettaCarburanteSafe.value = 0;
    iniettaCarburanteLapPlus.value = 0;
    consumoCarburante.value = '';
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
<span class="label label-text  md:w-2/5 mx-auto">Tempo sul giro</span>

<div class="flex flex-row mx-auto md:w-2/5 w-full">
      
    <div class="basis-1/3 mr-2">
        <label class="input input-bordered input-primary flex gap-2 items-center">
            mm <input type="number" v-model="lapTimeMinutes" placeholder="mm" class="w-full m-0" />
        </label>
    </div>

    <span class="mr-2 mt-2">:</span>

    <div class="basis-1/3 mr-2">
        <label class="input input-bordered input-primary flex gap-2 items-center">
            ss <input type="number"  v-model="lapTimeSeconds" placeholder="ss" class=" w-full m-0" />
        </label>  
    </div>

    <span class="mr-2 mt-2">:</span>

    <div class="basis-1/3 ">
        <label class="input input-bordered input-primary flex gap-2 items-center">
            ms <input type="number" placeholder="ms" v-model="lapTimeMilliseconds" class="w-full m-0" />
        </label>
    </div>
    
</div>
  
<span class="label label-text mt-5  md:w-2/5 mx-auto">Durata della gara</span>

<div class="flex flex-row mx-auto md:w-2/5 w-full">
      
    <div class="basis-1/2 w-full mr-2">
        <label class="input input-bordered  input-primary flex items-center gap-2">
            h <input type="number" v-model="raceTimeHours" placeholder="hh" class="m-0" />
        </label>
    </div>

    <span class="mr-2 mt-2">:</span>

    <div class="basis-1/2 w-full">
        <label class="input input-bordered  input-primary flex items-center gap-2">
            m <input type="number" v-model="raceTimeMinutes" placeholder="mm" class="m-0" />
        </label>
    </div>
    
</div>

   
<span class="label label-text mt-5  md:w-2/5 mx-auto">Consumo carburante per giro</span>
    <div class="w-full md:w-2/5 mx-auto ">
    <label class="input input-bordered  input-primary flex items-center gap-2">
        L <input v-model="consumoCarburante"  type="number" class="grow" placeholder="L"/>
        <!-- <kbd @click="addProductFromIcon(productInput)" class="kbd kbd-sm">Enter</kbd> -->
    </label>
    </div>

    <div class="flex flex-row mx-auto md:w-2/5 w-full mt-10">

        <span @click="CalcolaBenzina" class="basis-1/3 mx-auto btn-secondary btn w-full">Calcola carburante da imbarcare</span>
        <span @click="ResettaDati" class="basis-1/3 btn-secondary mx-auto btn w-full">Resetta dati</span>
    </div>



    <div class="flex flex-row mx-auto md:w-2/5 w-full ">
      
      <div class="basis-1/3 mr-2 flex items-center ml-5">
        <span class="label label-text md:w-2/5 ">Carburante minimo</span>
        
        <span class="label label-text md:w-3/5 ">
            <label class="input input-bordered flex items-center gap-2">
          
                <span class="grow">
                    L {{ iniettaCarburante }}
                </span>
         
            </label>
        </span>
      </div>
  
      <div class="basis-1/3 mr-2 flex items-center">
        <span class="label label-text md:w-2/5 ">Carburante sicuro</span>
        
        <span class="label label-text md:w-3/5 ">
            <label class="input input-bordered flex items-center gap-2">
          
                <span class="grow">
                    L {{ iniettaCarburanteSafe }}
                </span>
         
            </label>
        </span>
      </div>
  
      <div class="basis-1/3 flex items-center">
        <span class="label label-text md:w-2/5">Con giro di lancio </span>
        
        <span class="label label-text md:w-3/5">
            <label class="input input-bordered flex items-center gap-2">
          
                <span class="grow">
                    L {{ iniettaCarburanteLapPlus }}
                </span>
         
            </label>
        </span>
      </div>
      
  </div>





</template>