<template>
  <div class="home">
    <img class="" alt="Vue logo" src="../assets/logo.png">
    <HelloWorld msg="Bienvenidos a la aplicacion de tareas con VUE"/>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'HomeView',
  components: {
    HelloWorld
  }
}
</script>
