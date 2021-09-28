<template>
  <div class="cast-container">
    <span v-for="(actor, index) in getCast(type, id)" :key="index">
      <span v-if="index < 4">{{ actor }}, </span>
      <span v-else>{{ actor }}...</span>
    </span>
  </div>
</template>

<script>
import axios from "axios";
export default {
  props: ["id", "type"],
  data() {
    return {
      cast: []
    };
  },
  methods: {
    getCast(type, id) {
      if(type === 'movie'){
        axios
        .get(
          "https://api.themoviedb.org/3/movie/" +
            id +
            "/credits?api_key=8aeadd2568b18f3ed669ace3260041bb"
        )
        .then((res) => {
          let castArray = res.data.cast;
          castArray.forEach((element) => {
            if (this.cast.length < 5) {
              this.cast.push(element.name);
            }
          });
        });
        return this.cast;
      }else if(type === 'tv'){
        axios
        .get(
          "https://api.themoviedb.org/3/tv/" +
            id +
            "/credits?api_key=8aeadd2568b18f3ed669ace3260041bb"
        )
        .then((res) => {
          let castArray = res.data.cast;
          castArray.forEach((element) => {
            if (this.cast.length < 5) {
              this.cast.push(element.name);
            }
          });
        });
        return this.cast;
      }
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
@import '../styles/general';
.cast-container {
  display: inline;
  color: $white;
}
</style>