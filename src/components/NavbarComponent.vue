<template>
  <header>
      <button>Inicio</button>
      <button>Perfil</button>
      <button class="btn btn-primary" @click="mostrarCarrito"> Carrito </button>
      <div v-if="mostrarVentanaCarrito" class="ventana-carrito">
          <button class="btn btn-primary" @click="cerrarVentanaCarrito"> Cerrar </button>
          <ul v-if="carritoLocal.length === 0">
              <li>No hay elementos en el carrito.</li>
          </ul>
          <ul v-else>
              <li v-for="item in carritoLocal" :key="item.id">
                  {{ item.titulo }} - {{ item.costo | price("$") }}
              </li>
          </ul>
          <div v-if="carritoLocal.length > 0" class="total-carrito">
              <button class="btn btn-danger" @click="vaciarCarrito">Vaciar Carrito</button>
              <p>Total a pagar: {{ calcularTotal() | price("$") }}</p>
          </div>
      </div>
  </header>
</template>

<script>
export default {
name: "NavbarComponent",
props: {
  carrito: {
    type: Array,
    default: () => []
  }
},
data() {
  return {
    mostrarVentanaCarrito: false,
    carritoLocal: []
  };
},
filters: {
  price(value, currency) {
    if (typeof value !== "number") return value;
    return `${currency}${value.toFixed(2)}`;
  }
},
methods: {
  mostrarCarrito() {
    this.carritoLocal = [...this.carrito]; // Hacer una copia local del carrito original
    this.mostrarVentanaCarrito = true;
  },
  cerrarVentanaCarrito() {
    this.mostrarVentanaCarrito = false;
  },
  vaciarCarrito() {
    this.carritoLocal = []; // Vaciar el carrito local
    this.$emit("carrito-actualizado", this.carritoLocal); // Emitir el evento con el carrito local vacío
  },
  calcularTotal() {
    return this.carritoLocal.reduce((total, item) => total + item.costo, 0);
  }
},
watch: {
  carrito: {
    immediate: true,
    handler() {
      this.carritoLocal = [...this.carrito];
    }
  }
}
};
</script>



<style scoped>
    header {
        position: fixed;
        background-color: gray;
        width: 100%;
        display: flex;
        justify-content: flex-end;
        align-items: center;
    }
    button {
        border: none;
        color: #fff;
        margin: 10px;
        background-color: transparent;
        font-size: 20px;
        font-family: Verdana, Geneva, Tahoma, sans-serif;
    }
.ventana-carrito {
    position: fixed;
    top: 60px; /* Ajusta la distancia según la altura del navbar */
    right: 0;
    height: 100vh;
    width: 30%;
    background-color: tan;
    color: black;
    padding: 20px;
    margin: 10px;
    text-align: center;
}

.ventana-carrito button {
    margin-bottom: 10px;
}
</style>