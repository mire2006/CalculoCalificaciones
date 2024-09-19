<template>
  <nav class="navbar navbar-expand-lg navbar-light bg-light">
    <div class="container-fluid"> 
      <a class="navbar-brand" href="#">Programación Frontend</a>
      <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav">
          <li class="nav-item">
            <router-link class="nav-link" :class="{ active: pestañaActiva === 'calculo' }" to="/">Cálculo de Calificaciones</router-link> 
          </li>
          <li class="nav-item">
            <router-link class="nav-link" :class="{ active: pestañaActiva === 'registro' }" to="/registro">Formulario de Registro</router-link> 
          </li>
        </ul>

        <form class="d-flex ms-auto"> 
          <input class="form-control me-2" type="search" placeholder="Search" aria-label="Search">
          <button class="btn btn-busqueda" type="submit">Búsqueda</button>
        </form>
      </div>
    </div>
  </nav>
</template>

<script>
export default {
  data() {
    return {
      pestañaActiva: 'calculo' 
    };
  },
  methods: {
    cambiarPestaña(pestaña) {
      this.pestañaActiva = pestaña;
    }
  }
};
</script>

<style scoped>
.btn-busqueda {
  background-color: green;
  color: white;
}
</style>