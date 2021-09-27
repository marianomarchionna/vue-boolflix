<template>
    <div class="single-card">
        <div class="film">
            <img v-if="singleFilm.poster_path!=null" :src="`https://image.tmdb.org/t/p/w342${singleFilm.poster_path}`" :alt="singleFilm.title">
            <img v-else src="../assets/img/error.jpg" alt="ERRORE">
            <div class="description">
                <span><strong>Titolo:</strong> {{ singleFilm.title }}</span>
                <span><strong>Titolo originale:</strong> {{ singleFilm.original_title }}</span>
                <span><strong>Voto: </strong><i class="fas fa-star" v-for="(star, index) in getVote(singleFilm.vote_average)" :key="index"></i></span>
                <span class="overview"><strong>Overview:</strong> {{ singleFilm.overview }}...</span>
                <span class="flag"><strong>Lingua originale:</strong><country-flag :country="enFlag(singleFilm.original_language)"/></span>
            </div>
        </div>
    </div>
</template>

<script>
import CountryFlag from 'vue-country-flag'
export default {
  name: 'Film',
  props: ['singleFilm'],
  components: {
        CountryFlag
    },
    methods:{
        enFlag(language){
            if(language === "en") return "gb"
            return language
        },
        getVote(vote){
            vote = vote/2;
            vote = Math.ceil(vote);
            return vote;
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
@import '../styles/general';
.single-card{
    background-color: transparent;
    width: 200px;
    height: 300px;
    perspective: 1000px;
    .film {
        position: relative;
        width: 100%;
        height: 100%;
        transition: transform 0.6s;
        transform-style: preserve-3d;
        box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
        img, .description {
            position: absolute;
            width: 100%;
            height: 100%;
            -webkit-backface-visibility: hidden;
            backface-visibility: hidden;
            }
        img {
            display: block;
            object-fit: cover;
        }
        .description {
            padding: 20% 5px 5% 5px;
            border: 3px solid $gray;
            transform: rotateY(180deg);
            i {
                color: $yellow;
            }
            span {
                display: block;
            }
            .overview {
                width: 100%;
                height: 40%;
                overflow: hidden;
                text-overflow: ellipsis;
            }
            .flag {
                display: flex;
                align-items: center;
            }
        }
    }
}
.single-card:hover .film {
  transform: rotateY(180deg);
  background-color: $header-color;
  cursor: pointer;
  color: $white;
}
</style>