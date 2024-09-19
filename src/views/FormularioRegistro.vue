<template>
  <div class="container mt-4">
    <h2>Formulario de Registro</h2>

    <form @submit.prevent="enviarFormulario">
      <div class="row">
        <div class="col-md-6 mb-3">
          <label for="nombre">Nombre:</label>
          <input type="text" class="form-control" id="nombre" v-model="nombre" @input="validarNombre" :class="{ 'is-invalid': !!errors.nombre }"> 
          <div class="invalid-feedback">{{ errors.nombre }}</div>
        </div>
        <div class="col-md-6 mb-3">
          <label for="email">Correo:</label>
          <input type="email" class="form-control" id="email" v-model="email" @input="validarEmail" :class="{ 'is-invalid': !!errors.email }">
          <div class="invalid-feedback">{{ errors.email }}</div>
        </div>
      </div>

      <div class="row">
        <div class="col-md-6 mb-3">
          <label for="contrasena">Contraseña:</label>
          <input type="password" class="form-control" id="contrasena" :value="contrasena" @input="actualizarContrasena" :class="{ 'is-invalid': !!errors.contrasena }"> 
          <div class="invalid-feedback">{{ errors.contrasena }}</div>
        </div>
        <div class="col-md-6 mb-3">
          <label for="confirmarContrasena">Repetir Contraseña:</label>
          <input type="password" class="form-control" id="confirmarContrasena" v-model="confirmarContrasena" @input="validarConfirmacionContrasena" :class="{ 'is-invalid': !!errors.confirmarContrasena }">
          <div class="invalid-feedback">{{ errors.confirmarContrasena }}</div>
        </div>
      </div>

      <button type="submit" class="btn btn-success">Enviar</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      nombre: '',
      email: '',
      contrasena: '',
      confirmarContrasena: '',
      errors: {}
    };
  },
  methods: {
    enviarFormulario() {
      this.validarNombre();
      this.validarEmail();
      this.validarContrasena();
      this.validarConfirmacionContrasena();

      if (Object.keys(this.errors).length === 0) {
        alert('El registro se ha realizado correctamente');

        this.nombre = '';
        this.email = '';
        this.contrasena = '';
        this.confirmarContrasena = '';
        this.errors = {};
      }
    },
    validarNombre() {
      if (this.nombre.trim() === '') {
        this.errors.nombre = 'El campo nombre es requerido'; 
      } else {
        delete this.errors.nombre;
      }
    },
    validarEmail() {
      const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
      if (!emailRegex.test(this.email)) {
        this.errors.email = 'Ingrese un correo electrónico válido';
      } else {
        delete this.errors.email;
      }
    },
    validarContrasena() {
      if (this.contrasena.trim() === '') {
        this.errors.contrasena = 'El campo contraseña es requerido';
      } else if (this.contrasena.length < 6) {
        this.errors.contrasena = 'La contraseña debe tener al menos 6 caracteres';
      } else {
        delete this.errors.contrasena;
      }
    },
    validarConfirmacionContrasena() {
      if (this.confirmarContrasena.trim() === '') {
        this.errors.confirmarContrasena = 'El campo repetir contraseña es requerido'; 
      } else if (this.contrasena !== this.confirmarContrasena) {
        this.errors.confirmarContrasena = 'Las contraseñas no coinciden';
      } else {
        delete this.errors.confirmarContrasena;
      }
    },
    actualizarContrasena(event) {
      this.contrasena = event.target.value;
      this.validarContrasena(); 
    }
  }
};
</script>