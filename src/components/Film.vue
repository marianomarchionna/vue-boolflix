<template>
    <div class="single-card">
        <div class="film">
            <img :src="`https://image.tmdb.org/t/p/w342${singleFilm.poster_path}`" :alt="singleFilm.title">
            <div class="description">
                <span><strong>Titolo:</strong> {{ singleFilm.title }}</span>
                <span><strong>Titolo originale:</strong> {{ singleFilm.original_title }}</span>
                <span><strong>Voto:</strong> {{ singleFilm.vote_average }}</span>
                <span><strong>Lingua originale:</strong> {{ singleFilm.original_language }}</span>
            </div>
        </div>
    </div>
</template>

<script>
export default {
  name: 'Film',
  props: ['singleFilm']
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
        }
        .description {
            padding: 20% 5px 5% 5px;
            border: 3px solid $gray;
            transform: rotateY(180deg);
            span {
                display: block;
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