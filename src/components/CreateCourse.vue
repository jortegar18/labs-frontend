<template>
    <div class="col-12 col-sm-10 col-md-8 offset-sm-1 offset-md-2">
      <div class="mt-5">
        <form class="border border-primary rounded form-inline" @submit="associate">
  
          <h2 class="col-12 text-center text-primary mt-3 mb-5">Crear un nuevo Curso</h2>
  
          <div class="form-group col-12">
            <label for="names" class="custom-label col-md-3">Nombre del Curso</label>
            <input id="names" class="form-control col-12 col-sm-10 col-md-7 offset-sm-1" type="text"
                   placeholder="Nombre" v-model="courseName" required/>
          </div>
  
          <div class="form-group col-12">
            <label class="custom-label col-md-3 display" for="horas">Horas</label>
            <input id="horas" class="form-control col-12 col-sm-10 col-md-7 offset-sm-1" type="text" placeholder="Horas" v-model="durationHours" required/>
              
          </div>
          <div class="col-12 mb-3">
            <button class="col-sm-6 col-md-4 offset-sm-5 offset-md-7 btn btn-primary" type="submit">
              Guardar
            </button>
          </div>
  
      </form>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import { getAuthenticationToken } from "@/dataStorage";


export default {
  name: "CreateCourse",
  data() {
    return {
      courseName: '',
      durationHours: null,
    };
  },
  methods: {
    associate(event) {
      // Validación básica de formulario
      
      if (!this.courseName || !this.durationHours) {
        alert('Por favor, complete todos los campos.');
        return;
      }
      // Llamada a la API de Spring para crear el curso
      const nuevoCurso = {
        courseName: this.courseName,
        durationHours: this.durationHours,
      };

  

      axios.post('http://localhost:9090/profesor/crear-curso', nuevoCurso,{ params: { access_token: getAuthenticationToken() }}) // Cambiar la URL según la configuración de tu backend de Spring
        .then(response => {
          console.log('Nuevo Curso creado:', response.data);
          // Reiniciar los campos del formulario
          this.courseName = '';
          this.durationHours = null;
        })
        .catch(error => {
          console.error('Error al crear el curso:', error);
        });
    },
  },
};
</script>



<style scoped>
  .form-inline .form-group{
    margin-bottom: 1rem;
  }
</style>


