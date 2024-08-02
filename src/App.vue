<template>
<div>
  <Score 
    :score="score"
    :record="record"
  />
  <Game 
    @update-score="updateScore"
  />
</div>
</template>

<script setup>
import { ref } from 'vue';
import Game from './components/Game.vue'
import Score from './components/Score.vue'

const score = ref(0);
const record = ref(0);

const updateScore = () => {
  score.value++;
  if(score.value > record.value) {
    record.value = score.value;
  }
}
</script>

<style lang="scss">
body {
  background: #2980b9;
  background: -webkit-linear-gradient(to right, #2980b9, #2c3e50); 
  background: linear-gradient(to right, #2980b9, #2c3e50);
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #0f151b;
  margin-top: 20px;
}
</style>
