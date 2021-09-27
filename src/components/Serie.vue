<template>
    <div class="single">
        <div class="serie">
            <img v-if="singleSerie.poster_path!=null" :src="`https://image.tmdb.org/t/p/w342${singleSerie.poster_path}`" :alt="singleSerie.title">
            <img v-else src="../assets/img/error.jpg" alt="ERRORE">
            <div class="description-serie">
                <span><strong>Titolo:</strong> {{ singleSerie.name }}</span>
                <span v-if="singleSerie.name!=singleSerie.original_name"><strong>Titolo originale:</strong> {{ singleSerie.original_name }}</span>
                <span><strong>Voto: </strong><i class="fas fa-star" v-for="(star, index) in getVote(singleSerie.vote_average)" :key="index"></i></span>
                <p class="overview-serie"><strong>Overview:</strong> {{ singleSerie.overview }}...</p>
                <span class="flag-serie"><strong>Lingua originale:</strong><country-flag :country="getFlag(singleSerie.original_language)"/></span>
            </div>
        </div>
    </div>
</template>

<script>
import CountryFlag from 'vue-country-flag'
export default {
  name: 'Serie',
  props: ['singleSerie'],
  components: {
        CountryFlag
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
.single{
    background-color: transparent;
    width: 200px;
    height: 300px;
    perspective: 1000px;
    .serie {
        position: relative;
        width: 100%;
        height: 100%;
        transition: transform 0.6s;
        transform-style: preserve-3d;
        box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
        img, .description-serie {
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
        .description-serie {
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
                max-height: 20%;
            }
            .overview-serie {
                width: 100%;
                height: 40%;
                overflow: hidden;
                text-overflow: ellipsis;
            }
            .flag-serie {
                display: flex;
                align-items: center;
            }
        }
    }
}
.single-serie:hover .serie {
  transform: rotateY(180deg);
  background-color: $header-color;
  cursor: pointer;
  color: $white;
}
</style>