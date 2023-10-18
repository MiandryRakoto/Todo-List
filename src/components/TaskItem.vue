<template>
    <div class="d-flex mb-3 ms-4 flex-row" v-for="(task, index) in  tasks " :key="index">
        <input class="form-check-input me-3" v-model="task.completed" type="checkbox">
        <p class="mt-0" role="button" :class="{ 'text-decoration-line-through': task.completed }">{{ task.title }}</p>
        <div class="d-flex">
            <button type="button" @click="getTaskToEdit(task)" data-bs-toggle="modal" data-bs-target="#staticBackdropEdit"
                class="btn px-2 mb-2 d-flex align-items-center btn-primary ms-3">
                <svg width="19px" height="19px" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg"
                    stroke="#ffffff">
                    <g id="SVGRepo_bgCarrier" stroke-width="0"></g>
                    <g id="SVGRepo_tracerCarrier" stroke-linecap="round" stroke-linejoin="round"></g>
                    <g id="SVGRepo_iconCarrier">
                        <path fill-rule="evenodd" clip-rule="evenodd"
                            d="m3.99 16.854-1.314 3.504a.75.75 0 0 0 .966.965l3.503-1.314a3 3 0 0 0 1.068-.687L18.36 9.175s-.354-1.061-1.414-2.122c-1.06-1.06-2.122-1.414-2.122-1.414L4.677 15.786a3 3 0 0 0-.687 1.068zm12.249-12.63 1.383-1.383c.248-.248.579-.406.925-.348.487.08 1.232.322 1.934 1.025.703.703.945 1.447 1.025 1.934.058.346-.1.677-.348.925L19.774 7.76s-.353-1.06-1.414-2.12c-1.06-1.062-2.121-1.415-2.121-1.415z"
                            fill="#ffffff"></path>
                    </g>
                </svg>
            </button>
            <button type="button" @click="getTaskToDelete(task)" data-bs-toggle="modal"
                data-bs-target="#staticBackdropDelete" class="btn px-2 mb-2 d-flex align-items-center btn-danger ms-2">
                <svg width="19px" height="19px" viewBox="0 0 1024 1024" xmlns="http://www.w3.org/2000/svg" fill="#ffffff"
                    stroke="#ffffff">
                    <g id="SVGRepo_bgCarrier" stroke-width="0"></g>
                    <g id="SVGRepo_tracerCarrier" stroke-linecap="round" stroke-linejoin="round"></g>
                    <g id="SVGRepo_iconCarrier">
                        <path fill="#ffffff"
                            d="M352 192V95.936a32 32 0 0 1 32-32h256a32 32 0 0 1 32 32V192h256a32 32 0 1 1 0 64H96a32 32 0 0 1 0-64h256zm64 0h192v-64H416v64zM192 960a32 32 0 0 1-32-32V256h704v672a32 32 0 0 1-32 32H192zm224-192a32 32 0 0 0 32-32V416a32 32 0 0 0-64 0v320a32 32 0 0 0 32 32zm192 0a32 32 0 0 0 32-32V416a32 32 0 0 0-64 0v320a32 32 0 0 0 32 32z">
                        </path>
                    </g>
                </svg>
            </button>
        </div>
        <DeleteModal id="staticBackdropDelete" @confirmed="deleteTask($event)" />
        <!-- Edit Tasks -->
        <div class="modal fade" id="staticBackdropEdit" tabindex="-1">
            <div class="modal-dialog">
                <div class="modal-content">
                    <div class="modal-header">
                        <label for="message-text" class="col-form-label me-2">Title</label>
                        <input type="text" class="modal-title" id="exampleModalLabel" v-model="taskToEdit.title" />
                        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                    </div>
                    <div class="modal-body">
                        <form>
                            <div class="mb-3">
                                <label for="message-text" class="col-form-label">Description</label>
                                <textarea class="form-control" id="message-text" v-model="taskToEdit.desc"></textarea>
                            </div>
                            <div class="mb-3">
                                <input class="form-check-input me-2" id="done" type="checkbox"
                                    v-model="taskToEdit.completed">
                                <label for=" done" class="form-label">Done</label>
                            </div>
                        </form>
                    </div>
                    <div class="modal-footer">
                        <button type="button" class="btn btn-light" data-bs-dismiss="modal">Close</button>
                    </div>

                </div>
            </div>
        </div>
    </div>
</template>
<script>
import DeleteModal from "./modals/DeleteModal.vue"
export default {
    components: {
        DeleteModal,
    },
    data() {
        return {
            taskDeleteIndex: 0,
            taskToEdit: {}
        }
    },
    props: {
        tasks: Array
    },
    methods: {
        getTaskToEdit(task) {
            this.taskToEdit = task;
        },
        getTaskToDelete(task) {
            this.taskDeleteIndex = this.tasks.indexOf(task);
        },
        deleteTask() {
            this.$emit("delete-task", this.taskDeleteIndex)
        }
    }
}
</script>