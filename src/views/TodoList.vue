<template>
    <div class="container mt-lg-5 border border-2 border-primary background-edit rounded">
        <h2 class="text-center">My To-do List</h2>
        <TaskList />
    </div>
</template>
<script>
import TaskList from "../components/TaskList"

export default {
    name: 'TodoApp',
    components: {
        TaskList
    }
}
</script>
<style>
.background-edit {
    background-color: rgb(185, 217, 245);
}
</style>