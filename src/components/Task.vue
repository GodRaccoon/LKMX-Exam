<template>
    <div>
        <li class="d-flex align-items-center list-group-item">
            <button
                class="btn border-0 flex-grow-1 text-left shadow-none"
                :class="{completed}"
                @click="$emit('on-toggle')"
                v-if="!isEditing"
            >
                <span>{{description}}</span>
            </button>
            
            <form v-else class="flex-grow-1" @submit.prevent="finishEditing()">
                <input
                    type="text"
                    class="form-control"
                    v-model="newTaskDescription"
                    @blur="finishEditing()"
                    ref="newTask"
                />
            </form>
            
            <button
                @click="startEditing()"
                class="btn btn-outline-primary border-0 ml-2"
            >
                <span class="fa fa-edit"></span>
            </button>

            <button @click="$emit('on-delete')" class="btn btn-outline-danger border-0">
                <span class="fa fa-trash"></span>
            </button>
        </li>

    </div>
</template>

<script>
    export default {
        data() {
            return {
                isEditing: false,
                newTaskDescription: ""
            };
        },
        
        props: {
            description: String,
            completed: Boolean
        },
        
        methods: {
            
            startEditing() {
                if (this.isEditing) {
                    this.finishEditing();
                } else {
                    this.newTaskDescription = this.description;
                    this.isEditing = true;
                    this.$nextTick(() => this.$refs.newTask.focus());
                }
            },
            
            finishEditing() {
                this.isEditing = false;
                this.$emit("on-edit", this.newTaskDescription);
            }
        }
    };
</script>

<style lang="scss" scoped>
    .completed {
        text-decoration: line-through;
    }
</style>