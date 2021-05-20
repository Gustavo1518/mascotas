<template>
  <div class="about">
    <nav class="navbar navbar-expand-lg navbar-light bg-light" >
  <div class="container">
    <a class="navbar-brand" href="#">REGISTRO DE ANIMAL</a>
  </div>
  <div class="alert alert-danger" v-if="error">
  {{error}}
</div>
</nav>
    <form action="" class="form">
          <div class="mb-3">
  <input type="text" class="form-control" id="nombre" placeholder="Nombre del animal" v-model="nombre">
</div><br/>
<div class="mb-3">
  <input type="text" class="form-control" id="raza" placeholder="Raza del animal" v-model="raza">
</div><br/>
  <div class="form-group">
    <label for="exampleFormControlFile1"> Subir imagen </label>
    <input type="input" class="form-control-file" id="img" v-model="img" >
  </div><br/>
  <div class="mb-3">
  <input type="text" class="form-control" id="color" placeholder="Color del animal" v-model="color">
</div><br/>
<select class="form-control" v-model="tamano">
  <option>Selecciona tamaño</option>
  <option v-for="(i) in catamano" :key="i.id">{{i.valor}}</option>
</select><br/>
<select class="form-control" v-model="peso">
  <option>Selecciona peso</option>
  <option v-for="(itempeso) in catPeso" :key="itempeso.id">{{itempeso.valor}}</option>
</select><br/>
<select class="form-control" v-model="edad">
  <option>Selecciona edad</option>
  <option v-for="(itemedad) in catEdad" :key="itemedad.id">{{itemedad.valor}}</option>
</select><br/>
<select class="form-control" v-model="genero">
  <option>Selecciona genero</option>
  <option v-for="(itemgenero) in catGenero" :key="itemgenero.id">{{itemgenero.valor}}</option>
</select><br/>
<div class="form-check">
  <input class="form-check-input" type="checkbox" value="" id="vacunas" v-model="vacunas">
  <label class="form-check-label" for="defaultCheck1">
    Si vacunado
  </label>
</div><br/>
<div class="form-check">
  <input class="form-check-input" type="checkbox" value="" id="defaultCheck2" disabled>
  <label class="form-check-label" for="defaultCheck2">
    No vacunado
  </label>
</div><br/>
   <div class="mb-3">
  <input type="text" class="form-control" id="comentario" placeholder="Agregar un comentario" v-model="comentario">
</div><br/>
<div class="button">
<button type="button" class="btn btn-primary btn-lg btn-block" @click="guardar()">Registrar</button>
</div>
    </form>
  </div>
</template>
<script>
import axios from 'axios'
export default {
  name: 'about',
  data () {
    return {
      info: null,
      nombre:
        this.$route.params.mascotas !== undefined
          ? this.$route.params.mascotas.nombre
          : '',
      raza:
        this.$route.params.mascotas !== undefined
          ? this.$route.params.mascotas.raza
          : '',
      img:
        this.$route.params.mascotas !== undefined
          ? this.$route.params.mascotas.img
          : '',
      color:
        this.$route.params.mascotas !== undefined
          ? this.$route.params.mascotas.color
          : '',
      comentario:
        this.$route.params.mascotas !== undefined
          ? this.$route.params.mascotas.comentario
          : '',
      tamano:
        this.$route.params.mascotas !== undefined
          ? this.$route.params.mascotas.tamano
          : '',
      peso:
        this.$route.params.mascotas !== undefined
          ? this.$route.params.mascotas.peso
          : '',
      edad:
        this.$route.params.mascotas !== undefined
          ? this.$route.params.mascotas.edad
          : '',
      genero:
        this.$route.params.mascotas !== undefined
          ? this.$route.params.mascotas.genero
          : '',
      vacunas: null,
      catPeso: null,
      catEdad: null,
      catGenero: null,
      catamano: null,
      error: false
    }
  },
  updated () {
    console.log('Formulario actualizado')
    console.log(this)
    console.log(this.$router)
    console.log(this.$route.params)
  },
  mounted () {
    this.getCatalogoPeso().then(response => {
      this.catPeso = response.data
    })
    this.getcatalogotamano().then(response => {
      this.catamano = response.data
    })
    this.getCatalogoEdad().then(response => {
      this.catEdad = response.data
    })
    this.getCatalogoGenero().then(response => {
      this.catGenero = response.data
    })
  },
  methods: {
    guardar () {
      this.verifyform()
      if (this.nombre === '' || this.raza === '' || this.color === '') {
        this.error = true; this.error = 'Campos Nombre, Raza, Color son obligatorios'
      } else {
        axios
          .post('http://localhost:3000/mascotas', {
            nombre: this.nombre,
            raza: this.raza,
            img: this.img,
            color: this.color,
            tamano: this.tamano,
            peso: this.peso,
            edad: this.edad,
            genero: this.genero,
            comentario: this.comentario,
            vacunas: false
          }).catch(error => console.log(error))
      }
    },
    getcatalogotamano () {
      return axios.get('http://localhost:3000/tamano')
    },
    getCatalogoPeso () {
      return axios.get('http://localhost:3000/peso')
    },
    getCatalogoEdad () {
      return axios.get('http://localhost:3000/edad')
    },
    getCatalogoGenero () {
      return axios.get('http://localhost:3000/genero')
    },
    verifyform () {
      setTimeout(() => {
        this.error = false
        console.log('prueba de reloj, hacia la alerta personalizada' + this.error)
      }, 5000)
    }
  }
}
</script>
<style>
.form {
 width: 500px;
 height: 500px;
 position: absolute;
 top: 15%;
 left: 37%;
}
.navbar-brand{
  right: 50px;
}
</style>
