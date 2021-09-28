<template>
    <div class="item-container">
        <div class="card">
            <div class="card-item">
                <img v-if="item.poster_path!=null" :src="`https://image.tmdb.org/t/p/w342${item.poster_path}`" :alt="item.title">
                <img v-else src="../assets/img/error.jpg" alt="ERRORE">
                <div class="description">
                    <span><strong>Titolo:</strong> {{ item.title || item.name }}</span>
                    <span v-if="item.title!=item.original_title || item.name!=item.original_name"><strong>Titolo originale:</strong> {{ item.original_title || item.original_name }}</span>
                    <span v-if="item.vote_average!=0"><strong>Voto: </strong><i class="fas fa-star" v-for="(star, index) in getVote(item.vote_average)" :key="index"></i></span>
                    <span v-else><strong>Voto non disponibile</strong></span>
                    <p v-if="item.overview!=''" class="overview"><strong>Overview:</strong> {{ item.overview }} </p>
                    <span v-else><strong>Overview non disponibile</strong></span>
                    <span class="flag"><strong>Lingua originale:</strong><country-flag :country="getFlag(item.original_language)"/></span>
                    <span v-if="item.name === undefined"><strong>Cast: </strong><Cast :type='movie' :id="item.id" /></span>
                    <span v-else-if="item.title === undefined"><strong>Cast: </strong><Cast :type='tv' :id="item.id" /></span>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import CountryFlag from 'vue-country-flag'
import Cast from "./Cast.vue";

export default {
  name: 'Item',
  props: ['item'],
  components: {
    CountryFlag,
    Cast
  },
  data() {
    return {
        movie: 'movie',
        tv: 'tv'
    }
  },
  methods:{
        getFlag(language){
            if(language === "en") 
                return "gb";
            else if(language === "ja")
                return "jpn";
            else 
                return language;
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
.card{
    font-size: 15px;
    background-color: transparent;
    width: 200px;
    height: 300px;
    perspective: 1000px;
    .card-item {
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
            padding: 5px;
            border: 3px solid $gray;
            transform: rotateY(180deg);
            i {
                color: $yellow;
            }
            span {
                display: block;
                overflow: hidden;
                text-overflow: ellipsis;
            }
            .overview {
                width: 100%;
                height: 30%;
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
.card:hover .card-item {
  transform: rotateY(180deg);
  background-color: $header-color;
  cursor: pointer;
  color: $white;
}
</style>