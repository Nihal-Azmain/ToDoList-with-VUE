<script setup>
    import { ref } from "vue"
    const prop =defineProps(['status'])
    defineEmits(['showRemainingTasks'])

    let color =ref("buttonface");
    if(prop.status==="remaining")color.value="cyan";
    else color.value ="buttonface";
    
</script>

<template>
    <button 
        @click="$emit('showRemainingTasks')"
        :style="{backgroundColor:color}"
    >Show Remaining Tasks</button>
</template>