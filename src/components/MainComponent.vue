<template>
  <main>
      <div class="container">
          <div class="item-container" v-for="item in items" :key="item.id">
          {{ item.titulo }}
          <img :src="item.portada" alt="Portada del artículo">
          {{ item.costo | price("$") }}
          <button class="btn btn-primary" @click="agregarAlCarrito(item)"> 
              {{ itemEnCarrito(item.id) ? 'En el carrito' : 'Añadir al carrito' }}
          </button>
          </div>
      </div>
  </main>
</template>

<script>

const items = [
  
  {
      id: 1,
      titulo: "Coctelera Boston",
      portada: require("../assets/cocteleraboston.jpg"),
      costo: 11500.00,
  },
  {
      id: 2,
      titulo: "Coctelera Cobbler",
      portada: require("../assets/cocteleracobbler.jpg"),
      costo: 10500.00,
  },
  {
      id: 3,
      titulo: "Coctelera Bahia",
      costo: 9750.00,
      portada: require("../assets/coctelerabahia.webp"),
  },
  {
      id: 4,
      titulo: "Jigger Japones",
      costo: 8000.00,
      portada: require("../assets/jigger.webp"),
  },
  {
      id: 5,
      titulo: "Colador Julep",
      costo: 3500.00,
      portada: require("../assets/coladorjulep.webp")
  },
  {
      id: 6,
      titulo: "Colador Oruga",
      costo: 4200.00,
      portada: require("../assets/coladororuga.webp")
  },
  {
      id: 7,
      titulo: "Cucharilla",
      costo: 2200.00,
      portada: require("../assets/cucharilla.webp")
  },
  {
      id: 8,
      titulo: "Destapador",
      costo: 800.00,
      portada: require("../assets/destapador.webp")
  },
  {
      id: 9,
      titulo: "Picos Dosificadores",
      costo: 500.00,
      portada: require("../assets/dosificadores.webp")
  },
  {
      id: 10,
      titulo: "Esterilla",
      costo: 4200.00,
      portada: require("../assets/esterilla.webp")
  },
  {
      id: 11,
      titulo: "Exprimidor",
      costo: 2600.00,
      portada: require("../assets/exprimidor.webp")
  },
  {
      id: 12,
      titulo: "Pala para hielo",
      costo: 1380.00,
      portada: require("../assets/palahielo.webp")
  },
  {
      id: 13,
      titulo: "Pinza de precision",
      costo: 980.00,
      portada: require("../assets/pinza.webp")
  },
  {
      id: 14,
      titulo: "Pizon",
      costo: 3080.00,
      portada: require("../assets/pizon.webp")
  },
  {
      id: 15,
      titulo: "Zester",
      costo: 1380.00,
      portada: require("../assets/zester.jpg")
  },
];

export default {
name: "MainComponent",
data() {
  return {
    items,
    carrito: []
  };
},
filters: {
  price(value, currency) {
    if (typeof value !== "number") return value;
    return `${currency}${value.toFixed(2)}`;
  }
},
methods: {
  agregarAlCarrito(item) {
    if (!this.itemEnCarrito(item.id)) {
      this.carrito.push(item);
      this.$emit("carrito-actualizado", this.carrito);
      console.log("Elemento agregado al carrito:", item);
    } 
    this.$emit("carrito-actualizado", this.carrito);
  },
  itemEnCarrito(itemId) {
    return this.carrito.some((item) => item.id === itemId);
  }
}
};
</script>
<style scoped>
    main {
        margin-top: 100px;
    }
    .container{        
        display: grid;
        grid-template-columns: 1fr 1fr 1fr 1fr;
        gap: 1rem;
    }
    .item-container{
        display: flex;
        flex-direction: column;
        align-items: center;
        background-color: #fff;
        color: black;
        padding: 10px;
        width: 200px;
        border-radius: 10px;
    }
    .item-container img{
        width: 100%;
    }
</style>