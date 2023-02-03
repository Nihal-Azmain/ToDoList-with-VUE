<script setup>
    import { ref } from "vue"
    const prop =defineProps(['status'])
    defineEmits(['showAllTasks'])

    let color =ref("buttonface");
    if(prop.status==="all")color.value="cyan";
    else color.value ="buttonface";
    
</script>

<template>
    <button 
        @click="$emit('showAllTasks')"
        :style="{backgroundColor:color}"
    >Show All Tasks</button>
</template>
