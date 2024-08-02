<template>
<div class="score">
    <h1>SIMON SAYS</h1>
    <div class="score__container">
        <h2>Текущий счет: {{ score }}</h2>
        <h2>Рекорд: {{ record }}</h2>
    </div>
</div>
</template>

<script setup>
import { defineProps } from 'vue';

const props = defineProps({
  score: {
    type: Number,
    default: 0
  },
  record: {
    type: Number,
    required: true
  }
});
</script>

<style lang="scss" scoped>
.score {
    padding: 0 20px;
    display: flex;
    justify-content: space-between;
    margin-bottom: 40px;

    &__container {
        display: flex;
        flex-direction: column;
        align-items: end;
    }
}
</style>