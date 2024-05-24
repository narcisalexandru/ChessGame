<template>
  <div
    :class="['cell']"
    :style="{ backgroundColor: color }"
    :draggable="!!content"
    @dragstart="onDragStart"
    @dragover.prevent
    @drop="onDrop"
  >
    <div v-if="content" class="content">{{ content }}</div>
  </div>
</template>

<script setup lang="ts">
const props = defineProps<{
  color: string,
  content?: string,
  rowIndex: number,
  colIndex: number
}>();

const emit = defineEmits<{
  (e: 'move-piece', from: { row: number, col: number }, to: { row: number, col: number }): void
}>();

const onDragStart = (event: DragEvent) => {
  event.dataTransfer?.setData('text/plain', JSON.stringify({ row: props.rowIndex, col: props.colIndex }));
};

const onDrop = (event: DragEvent) => {
  const data = event.dataTransfer?.getData('text/plain');
  if (data) {
    const from = JSON.parse(data);
    const to = { row: props.rowIndex, col: props.colIndex };
    emit('move-piece', from, to);
  }
};
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
  font-size: 60px;
}
</style>
