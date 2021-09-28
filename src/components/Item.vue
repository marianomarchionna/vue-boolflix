<template>
    <div class="item-container">
        <div class="card">
            <div class="card-item">
                <img v-if="item.poster_path!=null" :src="`https://image.tmdb.org/t/p/w342${item.poster_path}`" :alt="item.title">
                <img v-else src="../assets/img/error.jpg" alt="ERRORE">
                <div class="description">
                    <span><strong>Titolo:</strong> {{ item.title }}</span>
                    <span v-if="item.title!=item.original_title"><strong>Titolo originale:</strong> {{ item.original_title }}</span>
                    <span><strong>Voto: </strong><i class="fas fa-star" v-for="(star, index) in getVote(item.vote_average)" :key="index"></i></span>
                    <p class="overview"><strong>Overview:</strong> {{ item.overview }}...</p>
                    <span class="flag"><strong>Lingua originale:</strong><country-flag :country="getFlag(item.original_language)"/></span>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import CountryFlag from 'vue-country-flag'
export default {
  name: 'Item',
  props: ['item'],
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
.card{
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
                max-height: 20%;
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