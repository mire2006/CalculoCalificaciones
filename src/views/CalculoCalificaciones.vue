<template>
  <div> 
    <div class="container mt-4">
      <h2 class="text-center mb-4">Cálculo de Calificaciones</h2>

      <div class="row justify-content-center"> 
        <div class="col-md-6"> 
          <div class="mb-3" v-for="i in 3" :key="i">
            <div class="text-center"> <label :for="'nota' + i" class="form-label">Nota {{ i }}:</label> </div>
            <input type="number" class="form-control" :id="'nota' + i" v-model.number="notas[i - 1]" min="10" max="70" required
                   :class="{ 'is-invalid': erroresValidacion.notas[i - 1] !== '' }"
                   @input="validarNota(i - 1)">  </input> 
            <div class="invalid-feedback" v-if="erroresValidacion.notas[i - 1]">
              {{ erroresValidacion.notas[i - 1] }}
            </div>
          </div>

          <div class="mb-3">
            <div class="text-center"> <label for="asistencia" class="form-label">Asistencia (%):</label> </div>
            <input type="number" class="form-control" id="asistencia" v-model.number="asistencia" min="0" max="100" required
                   :class="{ 'is-invalid': erroresValidacion.asistencia !== '' }"
                   @input="validarAsistencia"> </input> 
            <div class="invalid-feedback" v-if="erroresValidacion.asistencia">
              {{ erroresValidacion.asistencia }}
            </div>
          </div>

          <div class="d-grid gap-2 col-6 mx-auto"> 
            <button class="btn btn-primary" @click="calcular">Calcular</button>
          </div>

          <div class="alert alert-danger mt-3" v-if="mostrarErrorGeneral">
            Por favor, ingrese valores válidos para las notas y la asistencia
          </div>

          <div class="mt-4" v-if="mostrarResultado">
            <p class="text-center">El promedio es: {{ promedio }}</p> 
            <p class="text-center">Tu estado es: {{ estado }}</p> 
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { mapState, mapActions } from 'vuex';

export default {
  data() {
    return {
      notas: [0, 0, 0],
      asistencia: 0,
      mostrarResultado: false,
      mostrarErrorGeneral: false,
      erroresValidacion: {
        notas: ['', '', ''],
        asistencia: ''
      },
      promedio: 0, 
      estado: ''    
    };
  },
  methods: {
    calcular() {
      this.validarCampos();

      if (this.camposValidos()) {
        const promedioPonderado = (this.notas[0] * 0.35) + (this.notas[1] * 0.35) + (this.notas[2] * 0.3);

        this.promedio = promedioPonderado.toFixed(2); 
        this.estado = (this.promedio >= 40 && this.asistencia >= 80) ? 'Aprobado' : 'Reprobado';

        this.mostrarResultado = true;
        this.mostrarErrorGeneral = false; 
      } else {
        this.mostrarErrorGeneral = true; 
      }
    },

    validarCampos() {
      for (let i = 0; i < this.notas.length; i++) {
        this.validarNota(i);
      }

      this.validarAsistencia();
    },

    validarNota(index) {
      if (this.notas[index] < 10 || this.notas[index] > 70) {
        this.erroresValidacion.notas[index] = 'La nota debe estar entre 10 y 70';
      } else {
        this.erroresValidacion.notas[index] = '';
      }
    },

    validarAsistencia() {
      if (this.asistencia < 0 || this.asistencia > 100) {
        this.erroresValidacion.asistencia = 'La asistencia debe estar entre 0 y 100';
      } else {
        this.erroresValidacion.asistencia = '';
      }
    },

    camposValidos() {
      return !this.erroresValidacion.notas.some(error => error !== '') && this.erroresValidacion.asistencia === '';
    }
  }
};
</script>

<style scoped>
.container {
  max-width: 700px;
}

h2 {
  font-weight: bold;
}

.btn-primary {
  background-color: #007bff;
  border-color: #007bff;
}
</style>