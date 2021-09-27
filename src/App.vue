<template>
  <div id="app">
    <Header @search="searchFilm"/>
    <FilmsList 
    :filmsList="filmsList"/>
    <SeriesList 
    :seriesList="seriesList"/>
    <div class="no-result" v-if="filmsList.length == 0 && seriesList.length == 0"><strong>NESSUN FILM O SERIE TV TROVATI CORRISPONDENTI ALLA SUA RICERCA</strong></div>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import FilmsList from './components/FilmsList.vue'
import SeriesList from './components/SeriesList.vue'
import axios from 'axios'

export default {
  name: 'App',
  components: {
    Header,
    FilmsList,
    SeriesList
  },
  data() {
    return {
      APIUrl: 'https://api.themoviedb.org/3/search/',
      APIKey: '8aeadd2568b18f3ed669ace3260041bb',
      input: "",
      filmsList: ['prova'],
      seriesList: ['prova']
    }
  },
  methods: {
    getMovie(){
      axios
      .get(this.APIUrl + 'movie?api_key=' + this.APIKey + '&query=' + this.input)
      .then(response => {
        this.filmsList='';
        this.filmsList=response.data.results;
      })
      .catch( err => {
        console.log("Error ", err);
      })
    },
    getSeries(){
      axios
      .get(this.APIUrl + 'tv?api_key=' + this.APIKey + '&query=' + this.input)
      .then(response => {
        this.seriesList='';
        this.seriesList=response.data.results;
      })
      .catch( err => {
        console.log("Error ", err);
      })
    },
    searchFilm(inputText){
      this.input = inputText;
      if(this.input!=""){
        this.getMovie();
        this.getSeries();
      }
    }
  },
  created(){
    this.getMovie();
    this.getSeries();
  }
}
</script>

<style lang="scss">
@import './styles/general';
.no-result {
  text-align: center;
  font-size: 20px;
}
</style>
