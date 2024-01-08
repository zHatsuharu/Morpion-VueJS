<script setup>
import Game from '@/components/GameMorpion.vue';
import {ref} from "vue";

const currentKey = ref(false);
</script>

<template>
  <Game :key="currentKey" />
  <button @click="currentKey = !currentKey">Reset</button>
</template>

<style scoped>
button {
  color: crimson;
  margin: 15px;
}
</style>