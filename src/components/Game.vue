<template>
<div class="game" @click="startGame">
    <div class="game__sectors">
        <Sector 
            v-for="(color, index) in colors"
            :key="index"
            :color="color"
            :activeColor="activeColor"
            @click="handleColorClick(color)"
        />
    </div>
</div>
</template>

<script setup>
import { ref, defineEmits } from 'vue';
import Sector from './Sector.vue'

const emit = defineEmits(['update-score']);

const isStarted = ref(false);
const level = ref(0);
const sequence = ref([]);
const playerSequence = ref([]);
const isPlayerTurn = ref(false);
const colors = ref(['green', 'red', 'blue', 'yellow']);
const activeColor = ref('');

const startGame = () => {
    if(!isStarted.value) {
        isStarted.value = true;
        addColorToSequence();
    }
}
const addColorToSequence = () => {
    const randomColor = colors.value[Math.floor(Math.random() * colors.value.length)];
    sequence.value.push(randomColor);
    playSequence();
}
const playSequence = async () => {
    isPlayerTurn.value = false;
    console.log(sequence.value);
    for (let color of sequence.value) {
        activeColor.value = color;
        await new Promise(resolve => setTimeout(resolve, 500));
        activeColor.value = '';
        await new Promise(resolve => setTimeout(resolve, 500));
    }
    isPlayerTurn.value = true;
}   
const handleColorClick = (color) => {
    if (!isPlayerTurn.value) return;
    playerSequence.value.push(color);
    if (playerSequence.value[playerSequence.value.length - 1] !== sequence.value[playerSequence.value.length - 1]) {
        alert('Game Over!');
        sequence.value = [];
        playerSequence.value = [];
        isStarted.value = false;
    } else if (playerSequence.value.length === sequence.value.length) {
        emit('update-score');
        playerSequence.value = [];
        addColorToSequence();
    }
}
</script>



<style lang="scss" scoped>
.game {
    position: relative;
    margin: auto;
    width: 70vw;
    height: 70vw;
    max-width: 600px;
    max-height: 600px;
    background-color: #184767;
    border-radius: 50%;
    padding: 20px;
    overflow: hidden;
    box-shadow: 0 0 30px 0 rgba(255, 255, 255, 0.275);

    &__sectors {
        position: relative;
        border-radius: 50%;
        width: 100%;
        height: 100%;
        overflow: hidden;
    }
}
</style>

