<script setup lang="ts">
import { ref } from 'vue'
import Square from './Square.vue';

const count = ref(0)

const squares = ref([
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9]
]);

const dataClicked = (dat:String) => console.log(dat);

</script>

<template>
  <div v-for="sqRow in squares">
    <Square v-for="sq in sqRow" :square-data="sq" @clicked="dataClicked" />
  </div>
</template>

<style scoped>
  div {
    display: flex;
  }
</style>
