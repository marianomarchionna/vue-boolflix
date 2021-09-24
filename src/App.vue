<template>
  <div id="app">
    <Header @search="searchFilm"/>
    <FilmsList 
    :filmsList="filmsList"/>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import FilmsList from './components/FilmsList.vue'
import axios from 'axios'

export default {
  name: 'App',
  components: {
    Header,
    FilmsList
  },
  data() {
    return {
      APIUrl: ('https://api.themoviedb.org/3/search/movie?api_key=8aeadd2568b18f3ed669ace3260041bb&query='),
      film: "",
      filmsList:[],
    }
  },
  methods: {
    getMovie(){
      axios
      .get(this.APIUrl+this.film)
      .then(response => {
        this.filmsList=response.data.results;
      })
      .catch( err => {
        console.log("Error ", err);
      })
    },
    searchFilm(inputText){
      this.film = inputText;
      if(this.film!=""){
        this.getMovie();
      }
    }
  },
  created(){
    this.getMovie();
  }
}
</script>

<style lang="scss">
@import './styles/general';
</style>
