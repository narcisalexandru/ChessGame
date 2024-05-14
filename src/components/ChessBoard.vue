<template>
    <div class="board">
      <div v-for="(row, rowIndex) in 8" :key="rowIndex" class="row">
        <ChessCell
          v-for="(col, colIndex) in 8"
          :key="colIndex"
          :color="getColor(rowIndex, colIndex)"
        />
      </div>
    </div>
  </template>
  
  <script lang="ts">
  import { defineComponent } from 'vue';
  import ChessCell from '@/components/ChessCell.vue';
  
  export default defineComponent({
    components: {
      ChessCell
    },
    methods: {
      getColor(rowIndex: number, colIndex: number): 'white' | 'black' {
        // Dacă suma indexului rândului și al indexului coloanei este un număr par, returnăm 'white', altfel 'black'
        return (rowIndex + colIndex) % 2 === 0 ? 'white' : 'black';
      }
    }
  });
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
    display: flex; /* Așază celulele pe același rând */
  }
  </style>
  