<script setup>
import { ref, onUpdated, defineEmits } from 'vue'
import Block from './Components/block.vue'
var hideStartButton = ref(false);  
var picked = ref('none');
var propPassed = ref(false);
  
  function end(){
    location.reload();
  }
  
</script>
   
<template>
  
  <main v-if="!hideStartButton">
    <div id="aboutMe">
      Daniel Duclos
      <a target="_blank" href="https://github.com/DanielD2004">
          <button id="github">Github</button>
      </a>
    </div>
    <div  id="gameModeSelector">
      <h1>Pick a Gamemode</h1>
      <!-- picked variable holds the value of selected button-->
      <input type="radio" id="survival" value="Survival" v-model="picked" />
      <label for="survival">Survival</label>
      <input type="radio" id="countdown" value="Countdown" v-model="picked" />
      <label for="countdown">Countdown</label>
      <button id="startButton" :disabled="picked == 'none'"   @click="propPassed = true; hideStartButton = true;">Start</button>
    </div>
    
  </main>
    <Block v-if="propPassed" :gameMode="picked" @gameOver="end()"/>
  
</template>

<style scoped>
  h1{
    background-color:rgb(251, 214, 165);
    text-align:center;
    font-size:100px;
    box-shadow: 5px 5px 5px black;
    border-radius:30px 0px 30px 0px;
    transform: rotate(-1deg);
  }
  
  input[type='radio'] { 
       transform: scale(2); 
       margin-left:45%;
       margin-bottom:20px;
   }

  label{
    margin-left:10px;
    transform: scale(2); 
    position:relative;
    font-weight:bolder;
  }
  
  #gameModeSelector{
    margin:auto;
    width:50%;
    align-items:auto;
    text-align:flex-start;
  }
  
  #aboutMe{
    margin-left:auto;
    margin-right:auto;
    position:relative;
    width:fit-content;
    padding:5px;
    border:1px solid black;
    border-radius:10px;
  } 

  #startButton{
    display: block;
    margin: auto;
    margin-top:20px;
    font-weight:bold;
    height:2vw;
    aspect-ratio:2;
    border-radius: 0px 10px 0px 10px;
    background-color:rgb(201, 245, 227);
    border:2px solid black;
    box-shadow: 2px 2px 1px rgb(48, 48, 48);
    cursor:pointer;
  }

  #startButton:disabled{
    background-color:rgb(115, 143, 143);
    color:white;
  }

</style>
