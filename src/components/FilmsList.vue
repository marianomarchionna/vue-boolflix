<template>
    <div class="container">
      <div class="single-film" v-for="(film, index) in filmsList" :key="index">
        <Film :key="index"  :singleFilm="film" />
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