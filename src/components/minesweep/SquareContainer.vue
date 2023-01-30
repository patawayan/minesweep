<script setup lang="ts">
import { ref } from "vue";

const emit = defineEmits(["clicked", ""]);
const props = defineProps({
  squareData: Number,
});
// const count = ref(0);
</script>

<template>
  <div
    @click="emit('clicked', props.squareData)"
    v-text="squareData == -1 ? 'X' : squareData || ' '"
  />
</template>

<style scoped lang="scss">
div {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 50px;
  height: 50px;
  border: solid 1px black;
}

div:hover {
  cursor: pointer;
  background-color: rgb(white, 50%);
}
</style>
