<script setup>
    import { ref } from "vue"
    const emit = defineEmits(['textValue']);
    const inputText=ref("");
    function emitText(e)
    {
        emit("textValue",inputText.value);
        inputText.value="";
        e.preventDefault();
    }
</script>

<template>
    <form id="inputForm">
            <input type="text" v-model="inputText" @keypress.enter="emitText">
            <button @click="emitText">ADD</button>
    </form>
</template>


<style scoped>
form{
    padding-bottom: 20px;
}
input{
    padding: 5px 5px;
}
</style>