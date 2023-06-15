<template>
  <div id="app">
    <NavbarComponent :carrito="carrito" @carrito-actualizado="actualizarCarrito"></NavbarComponent>
    <MainComponent :carrito="carrito" @carrito-actualizado="actualizarCarrito"></MainComponent>
    <FooterComponent mensaje="@ Sebastian Perez 2023"/>
  </div>
</template>

<script>
import NavbarComponent from './components/NavbarComponent.vue';
import MainComponent from './components/MainComponent.vue';
import FooterComponent from './components/FooterComponent.vue';

export default {
  name: 'App',
  components: {
    NavbarComponent,
    MainComponent,
    FooterComponent
  },
  data() {
    return {
      carrito: []
    }
  },
  methods: {
    actualizarCarrito(nuevoCarrito) {
      this.carrito = nuevoCarrito;
    }
  }
}
</script>


<style>
#app {
  font-family: Verdana, Geneva, Tahoma, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
