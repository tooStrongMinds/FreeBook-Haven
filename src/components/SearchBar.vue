<template>
    <span>
      <input type="search" placeholder="Search by Title or Author" id="searchInput" v-model="searchQuery" @input="onInput" >
      <i class="fa-solid fa-magnifying-glass"></i>
      </span>
  </template>
  
  <script>
  
  export default {
  name: 'SearchBar',
  data() {
      return {
          searchQuery: ''
      }
  },
  methods: {
      onInput() {
          this.$emit('search', this.searchQuery)
      }
  }
  }
  </script>

<style scoped>
span {
    background: #fffaf5;
    border-radius: 20px;
    height: 40px;
    width: 50%;
    padding-right: 30px;

    display: flex;
    align-items: center;
    justify-content: space-between;
}
input {
    border: none;
    outline: none;
    padding: 10px;
    font-size: 16px;
    background: transparent;
    width: 100%;
    margin: 0 auto;
    border-radius: 20px;
}
i {
    color: #e16a00;
    font-size: 20px; 
}
</style>