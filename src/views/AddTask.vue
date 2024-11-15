<template>
    <div class="container my-5">
        <h1 class="text-center mb-4">Agregar tarea</h1>
        <div class="input-group mb-3">
            <input
                v-model="newTask"
                @keyup.enter="addTask"
                placeholder="Añadir nueva tarea"
                class="form-control"
            />
            <button @click="addTask" class="btn btn-success">Agregar</button>
        </div>

        <ul v-if="tasks.length > 0" class="list-group">
            <li
                v-for="task in tasks"
                :key="task.id"
                class="list-group-item d-flex justify-content-between align-items-center"
            >
                <span :class="{ 'text-decoration-line-through text-muted': task.completed }">
                    {{ task.todo }}
                </span>
                <div>
                    <button
                        @click="toggleTaskCompletion(task)"
                        class="btn btn-sm"
                        :class="task.completed ? 'btn-warning' : 'btn-primary'"
                    >
                        {{ task.completed ? 'Desmarcar' : 'Completar' }}
                    </button>
                    <button @click="deleteTask(task)" class="btn btn-sm btn-danger ms-2">
                        Borrar
                    </button>
                </div>
            </li>
        </ul>
    </div>
</template>

<script>
export default {
    name: "AddTask",
    data() {
        return {
            newTask: "", // Campo de entrada para la nueva tarea
            tasks: [],   // Lista de tareas locales
        };
    },
    methods: {
        addTask() {
            if (this.newTask.trim() === "") return;

            const newTask = {
                todo: this.newTask,
                completed: false,
                id: Date.now(), 
            };

            // Añadir la nueva tarea al inicio de la lista
            this.tasks.unshift(newTask);
            this.newTask = ""; // Limpiar el campo de entrada después de agregar
        },

        // Elimina una tarea específica de la lista
        deleteTask(task) {
            this.tasks = this.tasks.filter((t) => t.id !== task.id);
        },

        // Cambia el estado de la tarea entre completada y no completada
        toggleTaskCompletion(task) {
            task.completed = !task.completed;
        },
    },
};
</script>

<style scoped>
/* Sin estilos personalizados; todo está hecho con clases de Bootstrap */
</style>