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
    <form>
            <input 
                type="text" v-model="inputText" 
                @keypress.enter="emitText" 
                autofocus
            >
            <button @click="emitText">ADD</button>
    </form>
</template>


<style scoped>
form{
    padding-bottom: 20px;
}
input{
    width: 600px;
    height: 25px;
    padding: 5px 5px;
    margin-right: 5px;
    text-align: center;
}

button{
    height: 38px;
}
</style>