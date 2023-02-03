<script setup>
    defineProps(['isSelected']);
    defineEmits(['select']);
</script>

<template>
    <button @click="$emit('select')">
        <span v-if="!isSelected">Select All</span>
        <span v-else>Unselect All</span>
    </button>
</template>