<script setup>
    import { ref } from "vue"
    const prop =defineProps(['status'])
    defineEmits(['showFinishedTasks'])

    let color =ref("buttonface");
    if(prop.status==="finished")color.value="cyan";
    else color.value ="buttonface";
    
</script>

<template>
    <button 
        @click="$emit('showFinishedTasks')"
        :style="{backgroundColor:color}"
    >Show Finished Tasks</button>
</template>