<template>
  <div id="app">
    <Header/>
    <FilmsList/>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import FilmsList from './components/FilmsList.vue'

export default {
  name: 'App',
  components: {
    Header,
    FilmsList
  }
}
</script>

<style lang="scss">
@import './styles/general';
</style>
