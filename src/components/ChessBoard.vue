<template>
  <div>
    <div class="theme-selector">
      <label for="color-theme">Select theme:</label>
      <select id="color-theme" v-model="selectedTheme">
        <option v-for="(theme, name) in themes" :key="name" :value="name">{{ name }}</option>
      </select>
    </div>
    
    <div class="board">
      <div v-for="(row, rowIndex) in board" :key="rowIndex" class="row">
        <ChessCell
          v-for="(cell, colIndex) in row"
          :key="colIndex"
          :color="getColor(rowIndex, colIndex)"
          :content="cell"
          :rowIndex="rowIndex"
          :colIndex="colIndex"
          @move-piece="movePiece"
        />
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { reactive, ref } from 'vue';
import ChessCell from '@/components/ChessCell.vue';

const themes = {
  'Default': { white: '#f0d9b5', black: '#b58863' },
  'Green Theme': { white: '#a9bfa8', black: '#21571b' },
  'Blue Theme': { white: '#add8e6', black: '#4682b4' },
  'Red Theme': { white: '#f4c4c0', black: '#8a251e' },
  'Pink Theme': { white: '#ffc0cb', black: '#cf1c7a' }
};

const selectedTheme = ref('Default');

const getColor = (rowIndex: number, colIndex: number): string => {
  const theme = themes[selectedTheme.value];
  return (rowIndex + colIndex) % 2 === 0 ? theme.white : theme.black;
};

const initialBoard = [
  ['♜', '♞', '♝', '♛', '♚', '♝', '♞', '♜'],
  ['♟', '♟', '♟', '♟', '♟', '♟', '♟', '♟'],
  [undefined, undefined, undefined, undefined, undefined, undefined, undefined, undefined],
  [undefined, undefined, undefined, undefined, undefined, undefined, undefined, undefined],
  [undefined, undefined, undefined, undefined, undefined, undefined, undefined, undefined],
  [undefined, undefined, undefined, undefined, undefined, undefined, undefined, undefined],
  ['♙', '♙', '♙', '♙', '♙', '♙', '♙', '♙'],
  ['♖', '♘', '♗', '♕', '♔', '♗', '♘', '♖'],
];

const board = reactive(initialBoard);

const movePiece = (from: { row: number, col: number }, to: { row: number, col: number }) => {
  const piece = board[from.row][from.col];
  if (piece) {
    board[from.row][from.col] = undefined;
    board[to.row][to.col] = piece;
  }
};
</script>

<style scoped>
.theme-selector {
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 2rem;
  gap: 5px;
}

.board {
  display: grid;
  align-items: center;
  justify-content: center;
  align-content: center;
}

.row {
  display: flex; 
}
</style>
