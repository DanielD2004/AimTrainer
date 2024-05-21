<script setup>
import { ref, onUpdated, defineEmits } from 'vue'
import Block from './Components/block.vue'
var hideStartButton = ref(false);  
var picked = ref('none');
var propPassed = ref(false);
  
  function end(){
    location.reload();
  }
  
  function passProp(){
    propPassed = true;
  }
  
</script>

<template>
  <header>
  </header>
  
  <main>
    
    <div v-if="!hideStartButton" id="gameModeSelector">
      <h1>Pick a Gamemode</h1>
      <!-- picked variable holds the value of selected button-->
      <input type="radio" id="survival" value="Survival" v-model="picked" />
      <label for="survival">Survival</label>
      
      <input type="radio" id="countdown" value="Countdown" v-model="picked" />
      <label for="countdown">Countdown</label>
      <button :disabled="picked == 'none'" v-if="!hideStartButton"  @click="passProp(); hideStartButton = true;">Start</button>
    </div>
    
    <Block v-if="propPassed" :gameMode="picked" @gameOver="end()"/>
  </main>
  
</template>

<style scoped>
  h1{
    text-align:center;
    font-family:monospace;
    font-size:100px;
   
  }
  
  input[type='radio'] { 
       transform: scale(2); 
   }

  label{
    margin-left:5px;
    margin-right:80px;
    transform: scale(2); 
    position:relative;
  }
  
  #gameModeSelector{
    margin:auto;
    width:50%;
    align-items:auto;
    text-align:center;
  }
  
  button{
    display: block;
    margin: auto;
    margin-top:50px;
    size:100%
  }
</style>
