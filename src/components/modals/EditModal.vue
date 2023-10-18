<template>
    <div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header">
                    <label for="message-text" class="col-form-label me-2">Title</label>
                    <input type="text" class="modal-title" id="exampleModalLabel" v-model="localTaskEdit.title" />
                    <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                </div>
                <div class="modal-body">
                    <form>
                        <div class="mb-3">
                            <label for="message-text" class="col-form-label">Description</label>
                            <textarea class="form-control" id="message-text" v-model="localTaskEdit.desc"></textarea>
                        </div>
                        <div class="mb-3">
                            <input class="form-check-input me-2" id="done" type="checkbox"
                                v-model="localTaskEdit.completed">
                            <label for=" done" class="form-label">Done</label>
                        </div>
                    </form>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Cancel</button>
                    <button type="button" @click="saveChanges(taskCopy)" class="btn btn-primary"
                        data-bs-dismiss="modal">Save</button>
                </div>

            </div>
        </div>
    </div>
</template>
<script>
export default {
    props: {
        taskEdit: Object
    },
    data() {
        return {
            localTaskEdit: { ...this.taskEdit }
        };
    },
    beforeMount() {
        // Copiez les valeurs initiales de taskEdit dans localTaskEdit
        this.localTaskEdit = { ...this.taskEdit };
    },
    methods: {
        saveChanges(newTask) {
            this.$emit("newTask", newTask)
        }
    },
}
</script>