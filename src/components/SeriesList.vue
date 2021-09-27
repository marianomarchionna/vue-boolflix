<template>
  <div class="serie-tv">
    <h2 v-if="seriesList.length>0">SERIE TV</h2>
    <div class="container-serie">
      <div class="single-serie" v-for="(serie, index) in seriesList" :key="index">
        <Serie :key="index"  :singleSerie="serie" />
      </div>
    </div>
  </div>
</template>


<script>
import Serie from './Serie.vue';

export default {
  name: 'SeriesList',
  props: ['seriesList'],
  components: {
    Serie
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
.serie-tv {
  margin-top: 100px;
  h2 {
    text-align: center;
    color: $boolflix-color;
    text-shadow: -1px 0 black, 0 1px black, 1px 0 black, 0 -1px black;
  }
  .container-serie {
    display: flex;
    flex-wrap: wrap;
    width: 80%;
    margin: 0 auto;
    justify-content: center;
    .single-serie {
      margin: 20px;
    }
  }
}
</style>