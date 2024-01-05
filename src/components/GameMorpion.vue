<template>
  <div class="container">
    <Board
      :turn="turn"
      @changeTurn="newTurn"
      @winnerFound="setWinner"
      @draw="setDraw"
    />
    <div class="text-center" v-if="winner === '' && !isDraw">
      <h2>Turn : {{turn}}</h2>
      <span>Click on a cell</span>
    </div>
    <div class="text-center" v-else-if="isDraw">
      <h2>Draw</h2>
    </div>
    <div class="text-center" v-else>
      <h2>Winner is {{ winner }} !</h2>
    </div>
  </div>
</template>

<script setup>

import Board from "@/components/BoardGame.vue";
import {ref} from "vue";

const turn = ref((['X', 'O'])[Math.round(Math.random())]);
const winner = ref('');
const isDraw = ref(false);
const newTurn = () => turn.value = turn.value === 'X' ? 'O' : 'X';
const setWinner = () => winner.value = turn.value;
const setDraw = () => isDraw.value = true;
</script>

<style scoped>
.container {
  display: flex;
  gap: 20px;
  align-items: center;
}
.text-center {
  text-align: center;
}
</style>