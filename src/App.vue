<template>
  <div id="app">
    <!-- Barra de navegación con enlaces a diferentes rutas -->  
    <nav class="navbar navbar-expand-lg navbar-light bg-success">
      <div class="container-fluid">        
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarText" aria-controls="navbarText" aria-expanded="false" aria-label="Toggle navigation">
          <span class="navbar-toggler-icon"></span>
        </button>

        <div class="collapse navbar-collapse" id="navbarText">
          <ul class="navbar-nav me-auto mb-2 mb-lg-0">
            <li class="nav-item">
              <router-link class="nav-link" to="/">
                <i class="bi bi-house-door"></i> Inicio
              </router-link>
            </li>
            <li class="nav-item">
              <router-link class="nav-link" to="/addtask">
                <i class="bi bi-plus-circle"></i> Agregar Tarea
              </router-link>
            </li>
            <li class="nav-item">
              <router-link class="nav-link" to="/tasklist">
                <i class="bi bi-clipboard-check"></i> Lista de tareas
              </router-link>
            </li>
            <li class="nav-item">
              <router-link class="nav-link" to="/combinedview">
                <i class="bi bi-table"></i> Lista combinada
              </router-link>
            </li>
          </ul>        
        </div>
      </div>
    </nav>
    <!-- Aquí se cargará el componente correspondiente a la ruta seleccionada -->
    <router-view/>
  </div>
</template>

<!-- Estilos -->
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 15px;
}

nav .nav-link {
  font-weight: bold;
  color: white;
  display: flex;
  align-items: center;
  gap: 10px;
}

nav .nav-link:hover {
  background-color: rgba(0, 0, 0, 0.1);
  border-radius: 5px;
}

nav i {
  font-size: 1.2rem;
}
</style>
