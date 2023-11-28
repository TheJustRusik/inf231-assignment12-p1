<script setup>
    import { ref, defineCustomElement } from "vue";
    import Task from "./components/Task.vue"
    
    let newTasksArray = ref([])
    let progressTasksArray = ref([])
    let finishedTasksArray = ref([])
    let titleInput;
    let msgInput;

    function createTask(){
        if (titleInput.length == 0){
            alert("Title is required!")
            return
        }
        newTasksArray.value.push({title: titleInput, msg: msgInput})
        titleInput = ""
        msgInput = ""
    }

    function deleteTask(index){
        newTasksArray.value.splice(index, 1)
    }
    
    function promoteToInProgres(index){
        progressTasksArray.value.push(newTasksArray.value[index])
        newTasksArray.value.splice(index, 1)
    }

    function promoteToFinished(index){
        finishedTasksArray.value.push(progressTasksArray.value[index])
        progressTasksArray.value.splice(index, 1)
    }
    
    function downgradeToNew(index){
        newTasksArray.value.push(progressTasksArray.value[index])
        progressTasksArray.value.splice(index, 1)
    }

    function downgradeToInProgres(index){
        progressTasksArray.value.push(finishedTasksArray.value[index])
        finishedTasksArray.value.splice(index, 1)
    }
</script>

<template>
    <div class="grid grid-cols-3 gap-4 p-4">
        <div>
            <div class="bg-[#fcfcfe] rounded-xl drop-shadow-md p-4">
                <div class="flex justify-start items-center">
                    <div>
                        <h2 class="text-4xl font-extrabold mb-4">Create task</h2>
                        <div class="xl:grid xl:grid-cols-3">
                            <p class="xl:text-right text-xl font-semibold">Title: </p>
                            <input v-model="titleInput" type="text" placeholder="Frontend" class="col-span-2 text-xl border-b-2 border-yellow-500 bg-transparent focus:outline-none focus:border-yellow-700">
                            <p class="xl:text-right text-xl font-semibold">Message: </p>
                            <input v-model="msgInput" type="text" placeholder="Do 12'th assignment" class="col-span-2 text-xl border-b-2 border-yellow-500 bg-transparent focus:outline-none focus:border-yellow-700">
                        </div>
                    </div>
                    <div class="mx-12 grid grid-cols-1">
                        <button class="mx-auto" @click="createTask">
                            <div class="bg-[#fddd00] rounded-full">
                                <img src="./assets/plus-svgrepo-com.svg" alt="" class="w-16 p-1 xl:p-4">
                            </div>
                            
                        </button>
                        
                        <p class="text-md font-extrabold text-center">Add Task!</p>
                    </div>
                </div>
            </div>
            <div class="bg-[#fcfcfe] rounded-xl drop-shadow-md mt-4 p-4">
                <h2 class="text-4xl font-extrabold">Current tasks: {{ newTasksArray.length == 0 ? "" : newTasksArray.length}}</h2>
                <Task v-for="(item, index) in newTasksArray" :title="item.title" :msg="item.msg" @delete="deleteTask(index)" @promote="promoteToInProgres(index)"></Task>
            </div>
        </div>
        <div>
            <div class="bg-[#fcfcfe] rounded-xl drop-shadow-md p-4">
                <h2 class="text-4xl font-extrabold">In-progress tasks: {{ progressTasksArray.length == 0 ? "" : progressTasksArray.length }}</h2>
                <Task v-for="(item, index) in progressTasksArray" :title="item.title" :msg="item.msg" @delete="downgradeToNew(index)" @promote="promoteToFinished(index)"></Task>
            </div>
        </div>
        <div>
            <div class="bg-[#fcfcfe] rounded-xl drop-shadow-md p-4">
                <h2 class="text-4xl font-extrabold">Finished tasks: {{ finishedTasksArray.length == 0 ? "" : finishedTasksArray.length}}</h2>
                <Task v-for="(item, index) in finishedTasksArray" :title="item.title" :msg="item.msg" @delete="downgradeToInProgres(index)"></Task>
            </div>
        </div>
    </div>
</template>
