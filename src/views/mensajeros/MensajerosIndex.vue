<template>
  <div class="container">
    <div class="row">
      <div class="col-md-12">
        <button type="button" class="btn btn-info" @click="limpiar()">
          Limpiar
        </button>
        <button type="button" class="btn btn-info" @click="getIndex()">
          Mostrar
        </button>
        <table class="table tabla-sm table-hover table-striped table-bordered">
          <thead>
            <tr>
              <th>Documento</th>
              <th>Nombre</th>
              <th>Fecha Nacimiento</th>
              <th colspan="2">Opciones</th>
            </tr>
          </thead>
          <tbody v-if="mensajeros.length > 0">
            <tr v-for="datos in mensajeros" :key="datos.id">
              <td>{{ datos.documento_id }}</td>
              <td :class="datos.nombre == 'Camilo' ? 'table-success': 'table-danger' ">
                {{ datos.nombre + " " + datos.apellido }}
              </td>
              <td>{{ datos.fecha_nacimiento }}</td>
            </tr>
          </tbody>
          <tbody v-else>
            <tr>
              <td colspan="5">
                <h5>No tiene datos...</h5>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      mensajeros: [],
    };
  },
  methods: {
    getIndex() {
      axios.get("http://127.0.0.1:8000/api/mensajeros").then((response) => {
        this.mensajeros = response.data.data;
      });
    },
    limpiar() {
      this.mensajeros = [];
    },
  },
  mounted() {
    //this.getIndex();
  },
};
</script>
