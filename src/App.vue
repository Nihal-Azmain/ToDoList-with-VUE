<script setup>
    import { ref , computed } from "vue"
    import inputTask from "./components/inputTask.vue"
    import TasksLists from "./components/tasksLists.vue";
    import allCompleted from "./components/allCompleted.vue"
    import showRemainingTasks from "./components/showRemainingTasks.vue";
    import showFinishedTasks from "./components/showFinishedTasks.vue"
    import showAllTasks from "./components/showAllTasks.vue"

    let id=0;
    const tasks=ref([]);
    const status=ref("all");
    const isAllSelected=computed(()=>{
        if(tasks.value.filter((task)=>{
            return task.isCompleted === false;
        }).length !== 0)return false;
        else return true;
    });
    
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
        if(text!=="")
        {
            tasks.value[taskId].value=text;
            // tasks.value[taskId].color="#f6f6f6";
            // tasks.value[taskId].isCompleted=false;
        }
        tasks.value[taskId].isEdit=false;
    }

    function toggleCompleted()
    {
        if(!isAllSelected.value)
        {
            for(let i=0;i<tasks.value.length;i++)
            {
                tasks.value[i].isCompleted=true;
                tasks.value[i].color="cyan"
            }
        }
        else 
        {
            for(let i=0;i<tasks.value.length;i++)
            {
                tasks.value[i].isCompleted=false;
                tasks.value[i].color="#f6f6f6"
            }
        }         
    }


    function showRemaining(){
        status.value="remaining"
    }

    function showAll(){
        status.value="all"
    }

    function showFinished(){
        status.value="finished"
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
                        :status="status"
                        @remove-task="removeTask"
                        @single-click="checkCompleted"
                        @double-click="switchTemplate"
                        @update-task="updateText"
            />
        </ul>

        <div>
            <allCompleted 
                :is-selected="isAllSelected" 
                @select="toggleCompleted" 
            />
            
            <showAllTasks :status="status" @show-all-tasks="showAll"/>
            <showRemainingTasks :status="status"  @show-remaining-tasks="showRemaining" />
            <showFinishedTasks  :status="status" @show-Finished-tasks="showFinished" />

        </div>
        
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