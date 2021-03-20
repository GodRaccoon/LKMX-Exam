<template>
    <div class="container">
        <div class="row">
            <div class="col-12 py-5">
                <h1>{{listName}}</h1>
            </div>
        </div>
        
        <div class="row mb-3">
            <create-task @on-new-task="addTask($event)" />
        </div>
        
        <div class="row">
            <div class="col-12 col-sm-10 col-lg-6">
                <ul class="list-group">
                    <task
                        v-for="(task, index) in tasks"
                        :key="index"
                        :description="task.description"
                        :completed="task.completed"
                        @on-toggle="toggleTask(task)"
                        @on-delete="deleteTask(task)"
                        @on-edit="editTask(task, $event)"
                    />
                </ul>
            </div>
        </div>
    </div>
</template>

<script>
    import Task from "./Task.vue";
    import CreateTask from "./CreateTask.vue";
    
    export default {
        
        props: {
            listName: String,
        },
        
        data() {
            return {
                backgroundColor:"#673AB7" ,
                //Ejemplos de tareas para que al correr la pagina ya tenga algunos ejemplos agregados
                tasks: [
                    {description: "Ejemplo tarea 1: Hacer examen LKMX", completed: false },
                    {description: "Ejemplo tarea 2: Hacer tarea de IA", completed: false },
                    {description: "Ejemplo tarea 3: Bañar al perro", completed: false },
                ],
            };
        },
        
        methods: {
            //Metodo para añadir una nueva tarea escrita
            addTask(newTask) {
                this.tasks.push({ description: newTask, completed: false });
            },
            
            //Metodo para tachar una tarea ya añadida
            toggleTask(task) {
                task.completed = !task.completed;
            },
            
            //Metodo para borrar una tarea añadida a la lista
            deleteTask(deletedTask) {
                this.tasks = this.tasks.filter(task => task !== deletedTask);
            },
            
            //Metodo para editar una tarea añadida a la lista
            editTask(task, newTaskDescription) {
                task.description = newTaskDescription;
            },
        },
    
        components: { Task, CreateTask },
    };
</script>

<style scoped lang="scss"></style>