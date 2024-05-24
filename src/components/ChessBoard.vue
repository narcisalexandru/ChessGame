<template>
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
</template>

<script setup lang="ts">
import { reactive } from 'vue';
import ChessCell from '@/components/ChessCell.vue';

const getColor = (rowIndex: number, colIndex: number): 'white' | 'black' => {
  return (rowIndex + colIndex) % 2 === 0 ? 'white' : 'black';
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
.board {
  height: 100vh;
  display: grid;
  align-items: center;
  justify-content: center;
  align-content: center;
}

.row {
  display: flex; 
}
</style>
