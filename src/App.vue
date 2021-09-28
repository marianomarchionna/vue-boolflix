<template>
  <div id="app">
    <Header @search="searchFilm"/>
    <Main 
    :filmsList="filmsList"
    :seriesList="seriesList"
    @getCast="getCast"/>
    <div class="no-result" v-if="filmsList.length == 0 && seriesList.length == 0"><strong>NESSUN FILM O SERIE TV TROVATI CORRISPONDENTI ALLA SUA RICERCA</strong></div>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import Main from './components/Main.vue'
import axios from 'axios'

export default {
  name: 'App',
  components: {
    Header,
    Main
  },
  data() {
    return {
      APIUrl: 'https://api.themoviedb.org/3/search/',
      APIKey: '8aeadd2568b18f3ed669ace3260041bb',
      APIUrlCast: 'https://api.themoviedb.org/3/',
      input: "casa",
      filmsList: [],
      seriesList: [],
      cast: [],
      id: ""
    }
  },
  methods: {
    searchFilm(inputText){
      this.input = inputText;
      window.scrollTo(0, 0);
      if(this.input!=""){
        this.getMovie();
        this.getSeries();
      }
    },
    getCast(id, type){
      axios
      .get(this.APIUrlCast + type + '/' + id + '/credits?api_key=' + this.APIKey)
      .then(response => {
        this.cast=response.data;
        console.log(response.data)
      })
    },
    getMovie(){
      axios
      .get(this.APIUrl + 'movie?api_key=' + this.APIKey + '&query=' + this.input)
      .then(response => {
        this.filmsList=response.data.results;
      })
      .catch( err => {
        console.log("Error ", err);
      })
      this.getCast('movie')
    },
    getSeries(){
      axios
      .get(this.APIUrl + 'tv?api_key=' + this.APIKey + '&query=' + this.input)
      .then(response => {
        this.seriesList=response.data.results;
      })
      .catch( err => {
        console.log("Error ", err);
      })
      this.getCast('tv')
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
Header {
  position: fixed;
  top: 0;
  left: 0;
  z-index: 999;
}

.no-result {
  text-align: center;
  font-size: 20px;
}
</style>
