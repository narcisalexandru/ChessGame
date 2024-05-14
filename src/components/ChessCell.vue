<template>
    <div :class="['cell', color]">
    </div>
</template>

<script setup lang="ts">
import { defineProps } from 'vue';

const props = defineProps({
    color: String as 'white' | 'black', // Specificăm tipul proprietății color
    content: String
});
</script>

<style>
.cell {
    width: 100px;
    height: 100px;
    border: 1px solid black;
}

.white {
    background-color: #f0d9b5;
}

.black {
    background-color: #b58863;
}
</style>
