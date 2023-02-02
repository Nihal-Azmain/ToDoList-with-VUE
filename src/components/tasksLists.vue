<script setup>
    import { ref , computed } from "vue"
    
    const prop = defineProps(['viewTask']);
    const emit = defineEmits(['removeTask','singleClick','doubleClick','updateTask']);
    const inputText=ref("");
    let noOfClicks=0;
    let timer=null;
    function eventHandler()
    {
        noOfClicks++;
        if(noOfClicks===1)
        {
            timer=setTimeout(()=>{
                noOfClicks=0;
                emit('singleClick',prop.viewTask.id);
            },300);
        }
        else
        {
            clearTimeout(timer);
            noOfClicks=0;
            emit('doubleClick',prop.viewTask.id);
        }
    }


    function checkFunction()
    {
        return prop.viewTask.value!== null;
    }

    function emitText(e)
    {
        emit("updateTask",inputText.value,prop.viewTask.id);
        inputText.value="";
        e.preventDefault();
    }



</script>

<template>
    <li v-show="checkFunction()" @click="eventHandler()" :style="{backgroundColor: viewTask.color}">
        <input type="checkbox">
        <input type="text" v-model="inputText" v-if="viewTask.isEdit" @keypress.enter="emitText" >
        <span v-else>{{ viewTask.value }}</span>
        <span class="close" @click="$emit('removeTask',e,viewTask.id)">x</span>
    </li>
</template>

<style scoped>
.close {
    cursor: pointer;
    position: absolute;
    top: 50%;
    right: 0%;
    padding: 12px 16px;
    transform: translate(0%, -50%);
}

.close:hover{
    background: #bbb;
}

li {
    border: 1px solid #ddd;
    margin-top: -1px; /* Prevent double borders */
    background-color: #f6f6f6;
    padding: 12px;
    text-decoration: none;
    font-size: 18px;
    color: black;
    display: block;
    position: relative;
    width: 650px;
    height: 20px;
}

li:hover {
    background-color: #eee;
}

input[type="checkbox"] {
    display: none;
}
input[type="text"]{
    padding: 5px 5px;
}
</style>