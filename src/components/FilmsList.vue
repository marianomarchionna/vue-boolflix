<template>
  <div class="film">
    <h2 v-if="filmsList.length>0">FILM</h2>
    <div class="container">
      <div class="single-film" v-for="(film, index) in filmsList" :key="index">
        <Film :key="index"  :singleFilm="film" />
      </div>
    </div>
  </div>
</template>


<script>
import Film from './Film.vue';

export default {
  name: 'FilmsList',
  props: ['filmsList'],
  components: {
    Film
  },
  data() {
    return {
      
    }
  },
  methods: {
    
  },
  computed: {
        
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
@import '../styles/general';
.film {
  margin-top: 150px;
  h2 {
    text-align: center;
    color: $boolflix-color;
    text-shadow: -1px 0 black, 0 1px black, 1px 0 black, 0 -1px black;
  }
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
}
</style>