<template>
  <div class="TablaReporte">
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <div class="container">
        <a class="navbar-brand" href="#">REPORTE DE ANIMAL</a>
      </div>
    </nav>
    <div class="table-responsive">
      <table class="table">
        ...
      </table>
    </div>

    <div class="table-responsive-sm">
      <table class="table">
        ...
      </table>
    </div>

    <div class="table-responsive-md">
      <table class="table">
        ...
      </table>
    </div>
    <table class="table">
      <thead>
        <tr>
          <th scope="col">Nombre</th>
          <th scope="col">Raza</th>
          <th scope="col">Imagen</th>
          <th scope="col">Color</th>
          <th scope="col">tamaño</th>
          <th scope="col">Peso</th>
          <th scope="col">Edad</th>
          <th scope="col">Genero</th>
          <th scope="col">Vacunas</th>
          <th scope="col">Acciones</th>
          <th scope="col">Mas...Detalles</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, index) in info" :key="item.id">
          <th scope="row">{{index}} {{item.nombre}}</th>
          <td>{{item.raza}}</td>
          <td><img :src="item.img" height="80" width="80" /></td>
          <td>{{item.color}}</td>
          <td>{{item.tamano}}</td>
          <td>{{item.peso}}</td>
          <td>{{item.edad}}</td>
          <td>{{item.genero}}</td>
          <td>{{item.vacunas}}</td>
          <td>
          <b-button variant="danger" @click="eliminar(item.id)">Eliminar</b-button>
          </td>
          <td>
          <div>
          <b-button v-b-modal.modal-tall @click="information(id)">Comentarios</b-button>
          <b-modal id="modal-tall" title="Comentarios">>
          <p class="my-4" v-for="i in 1" :key="i">
            {{item.comentario}}
          </p>
          </b-modal>
          </div>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
<script>
import axios from 'axios'
export default {
  name: 'about',
  data () {
    return {
      info: null
    }
  },
  mounted () {
    this.getmascotas()
  },
  methods: {
    eliminar (id) {
      axios.delete('http://localhost:3000/mascotas/' + id)
        .then(response => {
          this.getmascotas().then(response => {
            this.info = response.data
          })
        })
    },
    getmascotas () {
      axios
        .get('http://localhost:3000/mascotas')
        .then(response => (this.info = response.data))
        .catch(error => console.log(error))
    },
    information (id) {
      return this.info.comentario + id
    }
  }
}
</script>
