<template>
    <div class="container">
      <div class="single-film" v-for="(film, index) in filmsList" :key="index">
        <Film :key="index"  :singleFilm="film" />
      </div>
    </div>
</template>


<script>
import axios from 'axios';
import Film from './Film.vue';

export default {
  name: 'FilmsList',
  props: ['input'],
  components: {
    Film
  },
  data() {
    return {
      APIUrl: ('https://api.themoviedb.org/3/search/movie?api_key=8aeadd2568b18f3ed669ace3260041bb&query=ritorno'),
      filmsList: [],
    }
  },
  methods: {
    getFilms() {
      axios
          .get(this.APIUrl)
          .then( res => {
            this.filmsList = res.data.results;
            // console.log(res.data)
          })
          .catch( err => {
            console.log("Error ", err);
          })
    },
  },
  computed: {
        
  },
  created() {
    this.getFilms();
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
@import '../styles/general';
.container {
  display: flex;
  flex-wrap: wrap;
  width: 80%;
  margin: 0 auto;
  justify-content: center;
  .single-film {
    margin: 20px;
  }
}
</style>