<template>
    <div :class="['cell', color]">
      <div v-if="content" class="content">{{ content }}</div>
    </div>
</template>
  
<script setup lang="ts">
  const props = defineProps<{
      color: 'white' | 'black',
      content?: string
  }>();
</script>
  
<style>
.cell {
    width: 100px;
    height: 100px;
    border: 1px solid black;
    position: relative;
  }
  
.content {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    font-size: 24px;
  }

.white {
    background-color: #f0d9b5;
}

.black {
    background-color: #b58863;
}
</style>
  