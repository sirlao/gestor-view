<template>
    <div class="container my-5">
        <h1 class="text-center mb-4">Lista de Tareas</h1>
        <button @click="fetchTasks" class="btn btn-dark w-100 mb-3">Cargar tareas desde la API</button>

        <div v-if="tasks.length > 0" class="list-group">
            <div v-for="task in tasks" :key="task.id" class="list-group-item">
                <div class="d-flex justify-content-between align-items-center">
                    <div>
                        <h5 :class="{ 'text-decoration-line-through text-muted': task.completed }">
                            {{ task.todo }}
                        </h5>
                    </div>
                    <div>
                        <button
                            @click="toggleTaskCompletion(task)"
                            class="btn btn-sm"
                            :class="task.completed ? 'btn-warning' : 'btn-primary'"
                        >
                            {{ task.completed ? 'Desmarcar' : 'Completar' }}
                        </button>
                        <button @click="deleteTask(task)" class="btn btn-sm btn-danger ms-2">Borrar</button>
                    </div>
                </div>
            </div>
        </div>

        <p v-else class="text-center text-muted">No hay tareas cargadas. Haz clic en "Cargar Tareas".</p>
    </div>
</template>

<script>
import axios from "axios";

export default {
    name: "TaskList",
    data() {
        return {
            tasks: [], // Almacenamiento local de las tareas traídas de la API
        };
    },
    methods: {
        // Llamada para obtener las tareas desde la API externa
        async fetchTasks() {
            try {
                const response = await axios.get("https://dummyjson.com/todos");
                this.tasks = response.data.todos; // Asignar las tareas obtenidas al array local
            } catch (error) {
                console.error("Error al cargar las tareas:", error);
            }
        },

        // Cambiar el estado de una tarea (completada/no completada)
        toggleTaskCompletion(task) {
            task.completed = !task.completed;
        },

        // Eliminar la tarea seleccionada
        deleteTask(task) {
            this.tasks = this.tasks.filter((t) => t.id !== task.id);
        },
    },
};
</script>

<style scoped>
/* Aquí pueden agregar estilos personalizados para el componente. */
</style>
