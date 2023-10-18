<template>
    <div class=" mt-md-4 mb-md-4">
        <label for="newTask" class="form-label fs-4">New task</label>
        <div class="d-flex ms-4">
            <input type="text" v-model="newTask" @keyup.enter="addTask" class="form-control w-75" id="newTask">
            <button type="button" @click="addTask()" class="btn btn-primary mx-3">Add</button>
        </div>
        <p v-if="vide" class="text-danger ms-4">The field cannot be empty</p>
    </div>
    <h1 class="fs-4 mb-3">Tasks list</h1>
    <TaskItem :tasks="taskList" @delete-task="deleteConfirm" />
    <div class=" d-flex justify-content-between mt-5">
        <p>Number of tasks: {{ countTask }}</p>
        <p>Uncompleted tasks: {{ getUnCompleteTask }}</p>
    </div>
</template>
<script>
import TaskItem from "@/components/TaskItem.vue"

export default {
    components: {
        TaskItem
    },
    data() {
        return {
            newTask: "",
            taskList: [],
            vide: false,
            countTask: 0
        }
    },
    computed: {
        getUnCompleteTask() {
            return this.taskList.filter(task => !task.completed).length;
        }
    },
    methods: {
        addTask() {
            if (this.newTask.trim() !== "") {
                this.taskList.push({ title: this.newTask, desc: "", completed: false });
                this.vide = false
                this.countTask++
            } else this.vide = true;
            this.newTask = ""
        },
        deleteConfirm(taskIndex) {
            this.taskList.splice(taskIndex, 1);
            this.countTask--
        },
    }
}
</script>