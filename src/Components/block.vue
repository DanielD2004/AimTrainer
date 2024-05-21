<template>

  <div class="currentStats">
    <h1 id="timeLeft"> 
      Countdown: {{countdown}}
    </h1>

    <h1 id="currentScore">
      Current Score: {{score}}    
    </h1>
  </div>
  
  <div v-if="props.gameMode === 'Survival'" :style="{position:'absolute', top:yValue + 'px', left:xValue + 'px'}" @mouseover="incrementScore(); resetCountdown();" @mouseleave="stopScore(); startCountdown(2);" id="block">
  </div>

  <div v-if="props.gameMode === 'Countdown'" :style="{position:'absolute', top:yValue + 'px', left:xValue + 'px'}" @mouseenter="startCountdown(20)" @mouseover="incrementScore();" @mouseleave="stopScore();" id="block">
  </div> 
</template>

<script setup>
import { ref, onMounted, onUpdated, defineEmits, defineProps } from 'vue'
const emits = defineEmits(['gameOver'])
var countdown = props.gameMode === 'Survival' ? ref(2) : ref(20);
var xValue = ref(568)
var yValue = ref(300)
var score = ref(0);
var movementTimer = 0;
var scoreTimer = 0;
var test = 0;
var speed = 1000;
var countdownTimer = 0;
var flag = false;

const props = defineProps({
  gameMode: String  
});

function startCountdown(n){
  if (props.gameMode === 'Countdown' && countdownTimer != 0){
    return;
  }
  countdownTimer = setInterval(() => {countdown.value--;}, 1000);
}
  
function resetCountdown(){
  clearInterval(countdownTimer)
  countdown.value = 2;
}

function move(){
  movementTimer = setInterval(() => {
    
    // random point on screen, positive number
    var xRandom = Math.floor(Math.random() * window.innerWidth);
    var yRandom = Math.floor(Math.random() * window.innerHeight);  
     
    xValue.value = xRandom
    yValue.value = yRandom
    // time until next movement is between 400 and 1200ms
    speed = Math.floor(Math.random() * (1200-400) + 400);
  }, speed);
}

// increment score every 10 milliseconds
function incrementScore(){
  scoreTimer = setInterval(() => {score.value++;}, 10)
}

  function stopScore (){
    clearInterval(scoreTimer);
  }


  onUpdated(()=> {
    if (countdown.value < 0){
      resetCountdown();
      emits('gameOver');
    }
  })

  onMounted(() => {
    move();
  })
  
</script>

<style>
#block{
  background-color:black;
  width:80px;
  aspect-ratio:1;
  transition-duration:1s;
  margin: 0 auto;
  border-radius:50px;
}

  #block:hover{
    background-color:red;
  }

  .currentStats{
    width:100vw;
    padding-bottom:200px;
    text-align:center;
    align-items:center;    
  }
</style>
