<script setup>
    defineProps(['isAnySelected']);
    defineEmits(['clearSelected']);
</script>

<template>
    <button @click="$emit('clearSelected')">Clear All Completed tasks</button>
</template>