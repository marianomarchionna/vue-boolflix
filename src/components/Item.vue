<template>
    <div class="item-container">
        <div class="card">
            <div class="card-item">
                <img v-if="item.poster_path!=null" :src="`https://image.tmdb.org/t/p/w342${item.poster_path}`" :alt="item.title">
                <img v-else src="../assets/img/error.jpg" alt="ERRORE">
                <div class="description">
                    <!-- titolo -->
                    <span><strong>Titolo:</strong> {{ item.title || item.name }}</span>
                    <!-- titolo originale -->
                    <span v-if="item.title!=item.original_title || item.name!=item.original_name"><strong>Titolo originale:</strong> {{ item.original_title || item.original_name }}</span>
                    <!-- voto -->
                    <span v-if="item.vote_average!=0"><strong>Voto: </strong><i class="fas fa-star" v-for="(star, index) in getVote(item.vote_average)" :key="index"></i></span>
                    <span v-else><strong>Voto non disponibile</strong></span>
                    <!-- overview -->
                    <p v-if="item.overview!=''" class="overview"><strong>Overview:</strong> {{ item.overview }} </p>
                    <span v-else><strong>Overview non disponibile</strong></span>
                    <!-- lingua -->
                    <span class="flag"><strong>Lingua originale:</strong><country-flag :country="getFlag(item.original_language)"/></span>
                    <!-- cast -->
                    <span v-if="item.name === undefined">
                        <strong>Cast: </strong>
                            <p class="inline" v-for="(actor, index) in getCast(movie, item.id)" :key="index">{{actor}}.  </p>
                    </span>
                    <span v-else-if="item.title === undefined">
                        <strong>Cast: </strong>
                            <p class="inline" v-for="(actor, index) in getCast(tv, item.id)" :key="index">{{actor}}.  </p>
                    </span>
                    <!-- genere -->
                    <span v-if="item.name === undefined">
                        <strong>Genere: </strong>
                        <p class="inline" v-for=" (genre, index) in item.genre_ids" :key="index">{{checkGenre(movie, genre)}}.  </p>
                    </span>
                    <span v-else-if="item.title === undefined">
                        <strong>Genere: </strong>
                        <p class="inline" v-for=" (genre, index) in item.genre_ids" :key="index">{{checkGenre(tv, genre)}}.  </p>
                    </span>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import CountryFlag from 'vue-country-flag'
import axios from "axios";

export default {
  name: 'Item',
  props: ['item'],
  components: {
    CountryFlag
  },
  data() {
    return {
        movie: 'movie',
        tv: 'tv',
        cast: [],
        movieId: [],
        tvId:[]
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
        },
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
        },
        APIMovieGenre() {
            axios
            .get('https://api.themoviedb.org/3/genre/movie/list?api_key=8aeadd2568b18f3ed669ace3260041bb')
            .then(res => {
                this.movieId = res.data.genres;
                return this.movieId
            })
        },
        APITvGenre() {
            axios
            .get('https://api.themoviedb.org/3/genre/tv/list?api_key=8aeadd2568b18f3ed669ace3260041bb')
            .then(res => {
                this.tvId = res.data.genres;
                return this.tvId
            })
        },
        checkGenre(type, id) {
            if( type === 'movie'){
                for(let i = 0; i < this.movieId.length; i++){
                if(this.movieId[i].id === id)
                    return this.movieId[i].name
                }
            }else{
                for(let i = 0; i < this.tvId.length; i++){
                if(this.tvId[i].id === id)
                    return this.tvId[i].name
                }
            }
        }
    },
    created() {
        this.APIMovieGenre(),
        this.APITvGenre()
    },
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
                max-height: 18%;
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
.inline {
    display: inline;
}
.card:hover .card-item {
  transform: rotateY(180deg);
  background-color: $header-color;
  cursor: pointer;
  color: $white;
}
</style>