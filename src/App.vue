<template>
  <div id="app">
    <img src="./assets/logo.png">
    <h1>Curso</h1>
    <select v-model="selectedCountry">
      <option v-for="country in countries" v-bind:value="country.value" v-bind:key="country.id">{{ country.name}}</option>
    </select>
    <loader v-show="loading"/>
    <ul>
      <artist v-for="artist in artists" v-bind:artist="artist" v-bind:key="artist.id">{{artist.name}}</artist>
    </ul>
      
  </div>
</template>

<script>
import Artist from './components/Artist'
import getArtists from './api'
import Loader from './components/Loader'

export default {
  name: 'app',
  data () {
    return {
      artists : [],
      countries : [
        { name : 'Mexico', value : 'mexico'},
        { name : 'Argentina', value : 'argentina'},
        { name : 'España', value : 'spain'}
      ],
      selectedCountry : 'mexico',
      loading : true
    }
  },
  components : {
    Artist : Artist,
    Loader : Loader
  },
  methods : {
    refreshArtists () {
      const self = this
      this.loading = true
      this.artists =[]
      console.log('entro')
      getArtists(this.selectedCountry)
      .then(function (artists){
        self.artists = artists
        self.loading = false
      })
    }
  },
  mounted : function () {
    this.refreshArtists()
  },
  watch : {
    selectedCountry () {
      
      this.refreshArtists()
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
