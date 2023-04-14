<template>
  <div class="container-fluid mt-2">
    <h1>Bienvenido al dummy</h1>
    <button @click="mis_cursos">Mis cursos</button>
    <button @click="agregar_rol">Agregar rol</button>
    <button @click="roles_usuario">Roles de usuario</button>
    <button @click="nuevo_curso">Agregar nuevo curso</button>
    <div class="row">
      <router-view></router-view>
    </div>
  </div>
  
</template>



<script>
  import {getAuthenticationToken} from '@/dataStorage';

  export default{
    name: "Home",
    beforeCreate( ){
      if( !getAuthenticationToken( ) ){
        this.$router.push( {name: 'login'} )
      }
    },
    methods: {
    mis_cursos() {
      // Llama a `$router.push` para redireccionar a la ruta /mis-cursos
      this.$router.push('/mis-cursos');
    },
    agregar_rol() {
      // Llama a `$router.push` para redireccionar a la ruta /principal/nuevo-rol
      this.$router.push('/principal/nuevo-rol');
    },
    roles_usuario() {
      // Llama a `$router.push` para redireccionar a la ruta /principal/roles
      this.$router.push('/principal/roles');
    },
    nuevo_curso() {
      // Llama a `$router.push` para redireccionar a la ruta /principal/roles
      this.$router.push('/principal/nuevo-curso');
    }
    
  }
  }
</script>



<style>

</style>
