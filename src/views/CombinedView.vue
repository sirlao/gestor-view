<template>
    <div class="container my-5">
        <h1 class="text-center mb-4">Lista de Tareas</h1>

        <!-- Sección para agregar tarea -->
        <div class="input-group mb-3">
            <input
                v-model="newTask"
                @keyup.enter="addTask"
                placeholder="Añadir nueva tarea"
                class="form-control"
            />
            <button @click="addTask" class="btn btn-success">Añadir</button>
        </div>

        <!-- Botón para cargar tareas desde la API -->
        <button @click="fetchTasks" class="btn btn-primary w-100 mb-3">Cargar Tareas de la API</button>

        <!-- Lista de tareas -->
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

        <p v-else class="text-center text-muted">No hay tareas disponibles. Agrega una tarea o carga desde la API.</p>
    </div>
</template>

<script>
import axios from "axios";

export default {
    name: "TaskManager",
    data() {
        return {
            newTask: "", // Campo de entrada para la nueva tarea
            tasks: [],   // Lista de tareas (combinación de las locales y las de la API)
        };
    },
    methods: {
        // Agregar tarea local
        addTask() {
            if (this.newTask.trim() === "") return;

            const newTask = {
                todo: this.newTask,
                completed: false,
                id: Date.now(), 
            };

            this.tasks.unshift(newTask); // Añadir tarea al inicio de la lista
            this.newTask = ""; // Limpiar el campo de entrada
        },

        // Cargar tareas desde la API
        async fetchTasks() {
            try {
                const response = await axios.get("https://dummyjson.com/todos");
                this.tasks = [...response.data.todos, ...this.tasks]; // Combinar las tareas locales con las de la API
            } catch (error) {
                console.error("Error al cargar las tareas desde la API:", error);
            }
        },

        // Cambiar estado de una tarea
        toggleTaskCompletion(task) {
            task.completed = !task.completed;
        },

        // Eliminar tarea
        deleteTask(task) {
            this.tasks = this.tasks.filter((t) => t.id !== task.id);
        },
    },
};
</script>

<style scoped>
/* Sin estilos personalizados; se usan clases de Bootstrap */
</style>
