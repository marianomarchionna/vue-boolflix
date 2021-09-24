<template>
  <header>
    <span>BOOLFLIX</span>
    <form class="d-flex my-5">
      <input type="text" placeholder="Search FILM" v-model='inputText'>
      <button type="submit" @click.prevent="$emit('performSearch', inputText)">Search</button>
      <button @click.prevent="resetSearch">Reset</button>
    </form>
  </header>
</template>


<script>
export default {
  name: 'Header',
  components: {
  },
  data() {
    return {
      inputText: '',
    }
  },
  methods: {
    resetSearch() {
      this.inputText = '';
      this.$emit('performSearch', this.inputText);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
@import '../styles/general';
header {
  height: 100px;
  width: 100%;
  background-color: $header-color;
  display: flex;
  justify-content: space-between;
  align-items: center;
  span {
    color: $boolflix-color;
    font-weight: $bold;
    font-size: $big;
    margin-left: 20px;
  }
  form {
    margin-right: 20px;
  }
}
</style>
