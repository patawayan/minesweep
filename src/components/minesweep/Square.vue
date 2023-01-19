<script setup lang="ts">
import { ref } from 'vue'

const emit = defineEmits(['clicked', ''])
const {squareData} = defineProps({
  squareData: Number
})
const count = ref(0)
</script>

<template>
  <div @click="emit('clicked', squareData)" v-text="squareData" />
</template>

<style scoped lang="scss">
  div {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 100px;
    height: 100px;
    border: solid 1px black;
  }

  div:hover {
      cursor: pointer;
      background-color: rgb(white, 50%);
  }
</style>