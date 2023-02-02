<script setup>
    import {ref} from "vue"
    import inputTask from "./components/inputTask.vue"
    import TasksLists from "./components/tasksLists.vue";

    let id=0;
    const tasks=ref([]);

    const active=ref("all");
    
    function newTask(text)
    {
        if(text === "")return;
        tasks.value.push({
            id: id++,
            value: text,
            isCompleted: false,
            color: "#f6f6f6",
            isEdit: false
        });
    }

    function removeTask(e,taskId)
    {
        tasks.value[taskId].value=null;
    }

    function checkCompleted(taskId)
    {
        tasks.value[taskId].isCompleted = !tasks.value[taskId].isCompleted;
        if(tasks.value[taskId].isCompleted)tasks.value[taskId].color="cyan";
        else tasks.value[taskId].color="#f6f6f6";
    }

    function switchTemplate(taskId)
    {
        tasks.value[taskId].isEdit=true;
    }

    function updateText(text,taskId)
    {
        tasks.value[taskId].value=text;
        tasks.value[taskId].color="#f6f6f6";
        tasks.value[taskId].isCompleted=false;
        tasks.value[taskId].isEdit=false;
    }

</script>

<template>
    <main>
        <h1>To-Do APP</h1>

        <inputTask @text-value="newTask"/>

        <ul>
            <TasksLists v-for="task in tasks" 
                        :key="task.id" 
                        :viewTask="task"
                        @remove-task="removeTask"
                        @single-click="checkCompleted"
                        @double-click="switchTemplate"
                        @update-text="updateText"
            />
        </ul>

    </main>
    
</template>

<style scoped>
main{
    display: flex;
    align-items: center;
    flex-direction: column;
    justify-content: center;
}

ul {
    list-style-type: none;
    padding: 0;
    padding-bottom: 20px;
    margin: 0;
}

</style>

