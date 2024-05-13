<template>
  <div id="app" class="py-3">
    <main class="container">
      <header>
        <h1 class="text-center m-3">Catálogo de productos</h1>
      </header>
      <section class="row justify-content-center g-3">
        <div
          class="col-12 col-md-6 col-lg-4"
          v-for="producto in productos"
          :key="producto.id"
        >
          <div class="card">
            <img :src="producto.rutaImg" :alt="producto.nombre" />
            <div class="card-body">
              <h5 class="card-title">{{ producto.nombre }}</h5>
              <p class="card-text">Detalle: {{ producto.descripcionCorta }}</p>
              <div>
                <button
                  class="btn btn-primary"
                  data-bs-toggle="modal"
                  data-bs-target="#miModal"
                  :data-producto-id="producto.id"
                  @click="mostrar"
                >
                  Producto {{ producto.id }}
                </button>
              </div>
            </div>
          </div>
        </div>
      </section>
      <hr />
    </main>

    <section>
      <h2 class="m-3">Ejemplo botones</h2>
      <!-- Button trigger modal -->
      <button
        class="btn btn-primary m-3"
        data-bs-toggle="modal"
        data-bs-target="#miModal"
        data-producto-id="1"
        @click="mostrar"
      >
        Producto 1
      </button>
      <button
        class="btn btn-primary m-3"
        data-bs-toggle="modal"
        data-bs-target="#miModal"
        data-producto-id="2"
        @click="mostrar"
      >
        Producto 2
      </button>
    </section>

    <!-- Modal -->
    <div
      class="modal fade"
      id="miModal"
      tabindex="-1"
      aria-labelledby="miModalLabel"
      aria-hidden="true"
    >
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <h1 class="modal-title fs-5" id="miModal">
              {{ currentProducto.nombre }}
            </h1>
            <button
              type="button"
              class="btn-close"
              data-bs-dismiss="modal"
              aria-label="Close"
            ></button>
          </div>
          <div class="modal-body">
            <img
              :src="currentProducto.rutaImg"
              :alt="currentProducto.nombre"
              class="w-100"
            />
            <p>
              <span>Detalle:</span>
              {{ currentProducto.descripcionCorta }}
            </p>
          </div>
          <div class="modal-footer">
            <button
              type="button"
              class="btn btn-secondary"
              data-bs-dismiss="modal"
            >
              Cerrar
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  components: {},
  data() {
    return {
      productos: [
        {
          id: 1,
          nombre: "Producto 1",
          descripcionCorta: "Este es el producto 1",
          rutaImg: "./img/imagen1.jpeg",
        },
        {
          id: 2,
          nombre: "Producto 2",
          descripcionCorta: "Este es el producto 2",
          rutaImg: "./img/imagen2.jpeg",
        },
        {
          id: 3,
          nombre: "Producto 3",
          descripcionCorta: "Este es el producto 3",
          rutaImg: "./img/imagen3.jpeg",
        },
      ],
      currentProducto: {},
    };
  },
  methods: {
    mostrar: function (e) {
      let elemento = e.target;
      let productoId = elemento.dataset.productoId;
      console.log(productoId);
      let foundProducto = this.productos.find(
        (producto) => producto.id == productoId
      );
      if (foundProducto) {
        this.currentProducto = foundProducto;
        console.log(foundProducto);
      } else {
        alert("Producto no encontrado.");
      }
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
