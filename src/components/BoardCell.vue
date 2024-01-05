<template>
  <button @click="clickHandler">{{ value }}</button>
</template>

<script setup>
import {ref} from "vue";

const props = defineProps({
  id: Number,
  turn: String,
  ended: Boolean
});
const value = ref("");

const emit = defineEmits(['cellClicked']);

function clickHandler() {
  if (value.value === '' && !props.ended) {
    emit('cellClicked', props.id);
    value.value = props.turn;
  }
}
</script>

<style scoped>
button {
  width: 80px;
  height: 80px;
}
</style>