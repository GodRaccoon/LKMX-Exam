<template>
    <form class="col-12 col-sm-10 col-md-8 cl-lg-6" @submit.prevent="addTask()">
        <input
            v-model="newTask"
            type="text"
            class="form-control"
            placeholder="Crear nueva tarea ..."
        />
    </form>
</template>

<script>
    export default {
        data() {
            return {
                newTask: ""
            };
        },
        
        methods: {
            addTask() {
                if (this.newTask.length > 0) {
                    this.$emit("on-new-task", this.newTask);
                }
                this.newTask = "";
            }
        }
    };
</script>

<style lang="scss" scoped></style>