<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <div class="container">
      <div class="row">
        <div class="col-12">
          <h1 class="display-1 my-5">
            Esta es mi Primera Tabla de datos con Vue
          </h1>
          {{ getData() }}
          <h2>{{ notebook.procesador }}</h2>
        </div>
      </div>
      <div class="row">
        <div class="col-12">
          <table class="table table-striped">
            <thead>
              <tr>
                <th scope="col">#</th>
                <th scope="col">Comuna</th>
                <th scope="col">Id Comuna</th>
                <th scope="col">Id Provincia</th>
                <th scope="col">Id Region</th>
                <th scope="col">Provincia</th>
                <th scope="col">Región</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(trabajador, i) in trabajadores" :key="i">
                <td>{{ i + 1 }}</td>
                <td>{{ trabajador.comuna }}</td>
                <td>{{ trabajador.id_comuna }}</td>
                <td>{{ trabajador.id_provincia }}</td>
                <td>{{ trabajador.id_region }}</td>
                <td>{{ trabajador.provincia }}</td>
                <td>{{ trabajador.region }}</td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
//let saludo = "Hola Mundo";
//las funciones se declaran aca, pero deben declararse en una propiedad llamada method
//vmethod atajo
export default {
  name: "App",
  data() {
    return {
      saludo: "Hola Mundo!(Estoy dentro de Vue)",
      gatos: 2,
      casado: false,
      notebook: {
        procesador: "Amd Rysen 9 4900mhz",
      },
      trabajadores: [],
    };
  },
  created() {
    this.getData();
  },
  methods: {
    async getData() {
      try {
        const URL =
          "https://us-central1-apis-varias-mias.cloudfunctions.net/regiones_comunas";
        /*
        const URL = "./data.json";
        const request = await fetch(URL);
        https://us-central1-apis-varias-mias.cloudfunctions.net/regiones_comunas
        const data = await request.json();
        this.trabajadoresEntel = data; */
        const request = await axios.get(URL);
        this.trabajadores = request.data;
      } catch (error) {
        console.log(error);
      }
    },
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
