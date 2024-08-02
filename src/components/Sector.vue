<template>
    <div 
        class="game__sector"
        :class="{ [color]: true, 'active': activeColor === color }"
        @click="handleClick"
    ></div>
</template>

<script setup>
import { ref, defineProps, defineEmits } from 'vue';

const props = defineProps({
  color: {
    type: String,
    required: true
  },
  activeColor: {
    type: String,
    required: true
  }
});

const emit = defineEmits(['click']);

const handleClick = () => {
  emit('click');
};
</script>

<style lang="scss" scoped>
.game__sector {
    position: absolute;
    border: 0;
    width: 49%;
    height: 49%;
    overflow: hidden;
    opacity: 0.5;
    cursor: pointer;
    transition: 0.2s;

    &:hover {
        opacity: 1; 
        transition: 0.2s;
    }
}
.green {
    top: 0;
    left: 0;
    background: #34e89e;
}
.red {
    top: 0;
    right: 0;
    background: #ef3b36;
}
.blue {
    bottom: 0;
    right: 0;
    background: #1cb5e0;
}
.yellow {
    bottom: 0;
    left: 0;
    background: #ffc371;
}
.game__sector.active {
    opacity: 1;
    transition: 0.2s;
}
</style>