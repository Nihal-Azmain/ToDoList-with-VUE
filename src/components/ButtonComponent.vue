<script setup>
    import { ref } from "vue"
    const prop = defineProps(['object'])
    const emit = defineEmits(['showAllTasks','showFinishedTasks','ShowRemainingTasks'])
    // console.log(prop.object);
    function emitFunction()
    {
        if(prop.object.title==="Show All Tasks")
            emit("showAllTasks");
        if(prop.object.title==="Show Remaining Tasks")
            emit("ShowRemainingTasks");
        if(prop.object.title==="Show Finished Tasks")
            emit("showFinishedTasks");
    }
</script>

<template>
    <button 
        :class="{active : object.active}"
        @click="emitFunction" 
    >{{ object.title }}</button>
</template>

<style scoped>
.active{
    background-color: aquamarine;
}
</style>