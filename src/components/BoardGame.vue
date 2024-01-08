<template>
  <div class="board">
    <BoardCell
        @cellClicked="refreshGame"
        v-for="cell in cells"
        :key="cell"
        :id="cell"
        :ended="ended"
    />
  </div>
</template>

<script setup>

import BoardCell from "@/components/BoardCell.vue";
import {inject, ref, watch} from "vue";

const {turn, changeTurn} = inject('status');
const emit = defineEmits(['winnerFound', 'draw']);

const cells = ref([...Array(9)].map((_, index) => index));
const game = ref(Array(9));
const ended = ref(false);

function refreshGame(id) {
  const newBoard = [...game.value];
  newBoard[id] = turn.value;
  game.value = newBoard;
}

watch(game, () => {
  if (checkWinner()) {
    ended.value = true;
    emit('winnerFound');
  } else {
    if (drawCheck()) {
      emit('draw');
    } else {
      changeTurn();
    }
  }
});

function checkWinner() {
  let result = false;
  const lines = [
      [0, 1, 2],
      [3, 4, 5],
      [6, 7, 8],

      [0, 3, 6],
      [1, 4, 7],
      [2, 5, 8],

      [0, 4, 8],
      [2, 4, 6],
  ];
  lines.forEach(line => {
    const [a, b, c] = line;
    const currentBoard = game.value;
    if (
        currentBoard[a] === currentBoard[b] &&
        currentBoard[b] === currentBoard[c] &&
        currentBoard[a] !== undefined
    ) {
      result = true;
    }
  });
  return result;
}
function drawCheck() {
  return !game.value.some(cell => cell === undefined);
}
</script>

<style scoped>
.board {
  display: grid;
  grid-gap: 15px;
  grid-template-columns: repeat(3, 80px);
}
</style>