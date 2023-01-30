<script setup lang="ts">
import { ref } from "vue";
import SquareContainer from "./SquareContainer.vue";

// const count = ref(0);

interface BombLocInterface {
  [key: number]: { [key: number]: boolean };
}

function generateBombLocs(bombAmt = 10, length = 10, width = length) {
  let bombLoc: BombLocInterface = {};

  while (bombAmt > 0) {
    const randLen = Math.floor(Math.random() * length);
    const randWid = Math.floor(Math.random() * width);

    if (!bombLoc[randLen]) {
      bombLoc[randLen] = { [randWid]: true };
      bombAmt--;
    } else if (!bombLoc[randLen][randWid]) {
      bombLoc[randLen][randWid] = true;
      bombAmt--;
    }
  }

  return bombLoc;
}

function generateGrid(
  bombLoc: BombLocInterface = {},
  length = 10,
  width = length
) {
  const finalGridData: number[][] = [];

  for (let i = 0; i < length; i++) {
    const finalGridRow = [];
    for (let j = 0; j < width; j++) {
      if (bombLoc[i] && bombLoc[i][j]) {
        finalGridRow.push(-1);
      } else {
        const lenPrevStart = i - 1 >= 0 ? i - 1 : 0;
        const lenNextEnd = i + 1 < length ? i + 1 : length;
        const rowPrevStart = j - 1 >= 0 ? j - 1 : 0;
        const rowNextEnd = j + 1 < width ? j + 1 : width;

        let bombCount = 0;
        for (let x = lenPrevStart; x <= lenNextEnd; x++) {
          for (let y = rowPrevStart; y <= rowNextEnd; y++) {
            bombCount += bombLoc[x] && bombLoc[x][y] ? 1 : 0;
          }
        }
        finalGridRow.push(bombCount);
      }
    }

    finalGridData.push(finalGridRow);
  }

  return finalGridData;
}
const bombLocs = generateBombLocs();
const squares = ref(generateGrid(bombLocs));

const dataClicked = (dat: String) => console.log(dat);
</script>

<template>
  <div v-for="(sqRow, lenInd) in squares" :key="lenInd">
    <SquareContainer
      v-for="(sq, widInd) in sqRow"
      :square-data="sq"
      @clicked="dataClicked"
      :key="widInd"
    />
  </div>
</template>

<style scoped>
div {
  display: flex;
}
</style>
