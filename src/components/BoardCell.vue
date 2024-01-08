<template>
  <button @click="clickHandler">{{ value }}</button>
</template>

<script setup>
import {inject, ref} from "vue";

const {turn} = inject("status");
const props = defineProps({
  id: Number,
  ended: Boolean
});
const value = ref("");

const emit = defineEmits(['cellClicked']);

function clickHandler() {
  if (value.value === '' && !props.ended) {
    emit('cellClicked', props.id);
    value.value = turn.value;
  }
}
</script>

<style scoped>
button {
  width: 80px;
  height: 80px;
}
</style>