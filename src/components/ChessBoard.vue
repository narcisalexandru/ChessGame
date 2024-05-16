<template>
  <div class="board">
    <div v-for="(row, rowIndex) in 8" :key="rowIndex" class="row">
      <ChessCell
        v-for="(col, colIndex) in 8"
        :key="colIndex"
        :color="getColor(rowIndex, colIndex)"
        :content="getPiece(rowIndex, colIndex)"
      />
    </div>
  </div>
</template>

<script setup lang="ts">
import ChessCell from '@/components/ChessCell.vue';

const getColor = (rowIndex: number, colIndex: number): 'white' | 'black' => {
  return (rowIndex + colIndex) % 2 === 0 ? 'white' : 'black';
};

const getPiece = (rowIndex: number, colIndex: number): string | undefined => {
  // Piesele negre
  if (rowIndex === 0 && colIndex === 0) {
    return '♜';
  } 
  else if (rowIndex === 0 && colIndex === 1) {
    return '♞';
  } 
  else if (rowIndex === 0 && colIndex === 2) {
    return '♝';
  }
  else if (rowIndex === 0 && colIndex === 3) {
    return '♛'; 
  }
  else if (rowIndex === 0 && colIndex === 4) {
    return '♚';
  } 
  else if (rowIndex === 0 && colIndex === 5) {
    return '♝';
  } 
  else if (rowIndex === 0 && colIndex === 6) {
    return '♞';
  } 
  else if (rowIndex === 0 && colIndex === 7) {
    return '♜';
  } 
  else if (rowIndex === 1) {
    return '♟';
  }
 // Piesele albe 
  else if (rowIndex === 7 && colIndex === 7) {
    return '♖';
  } else if (rowIndex === 7 && colIndex === 6) {
    return '♘'; 
  } else if (rowIndex === 7 && colIndex === 5) {
    return '♗'; 
  } else if (rowIndex === 7 && colIndex === 4) {
    return '♕'; 
  } else if (rowIndex === 7 && colIndex === 3) {
    return '♔'; 
  } else if (rowIndex === 7 && colIndex === 2) {
    return '♗'; 
  } else if (rowIndex === 7 && colIndex === 1) {
    return '♘';
  } else if (rowIndex === 7 && colIndex === 0) {
    return '♖';
  } else if (rowIndex === 6) {
    return '♙'; 
  }
  
  return undefined;
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
