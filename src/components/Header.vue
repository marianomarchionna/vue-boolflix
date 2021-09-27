<template>
  <header>
    <span>BOOLFLIX</span>
    <form>
      <input type="text" placeholder="Search FILM or TV SERIES" v-model='inputText' @keyUp.enter="$emit('search', inputText)">
      <button type="submit" @click.prevent="$emit('search', inputText)"><strong>Search</strong></button>
      <button @click.prevent="resetSearch"><strong>Reset</strong></button>
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
    input {
      padding: 5px;
      padding-right: 75px;
      margin-right: 5px;
      border: none;
      border-radius: 5px;
    }
    button {
      cursor: pointer;
      padding: 5px 20px;
      margin: 0 5px;
      color: $white;
      background-color: $boolflix-color;
      border: none;
      border-radius: 5px;
    }
    button:hover {
      transform: scale(1.1);
    }
  }
}
</style>
