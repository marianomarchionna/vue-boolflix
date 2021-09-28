<template>
  <div class="container">
    <div class="item">
      <h2 v-if="filmsList.length>0">FILM</h2>
      <div class="container">
        <div class="single" v-for="(item, index) in filmsList" :key="index">
          <Item :item="item" />
        </div>
      </div>
    </div>
    <div class="item">
      <h2 v-if="seriesList.length>0">SERIE TV</h2>
      <div class="container">
        <div class="single" v-for="(item, index) in seriesList" :key="index">
          <Item :item="item" />
        </div>
      </div>
    </div>
  </div>
</template>


<script>
import Item from './Item.vue';

export default {
  name: 'Main',
  props: ['filmsList', 'seriesList'],
  components: {
    Item
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
  margin-top: 120px;
  .item {
    margin-top: 30px;
    h2 {
      text-align: center;
      color: $boolflix-color;
      text-shadow: -1px 0 black, 0 1px black, 1px 0 black, 0 -1px black;
    }
    .container {
      display: flex;
      flex-wrap: wrap;
      width: 80%;
      margin: 0 auto;
      justify-content: center;
      .single {
        margin: 20px;
      }
    }
  }
}
</style>