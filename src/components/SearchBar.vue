<template>
    <span v-if="isSearchBarVisible || isDesktop">
      <div class="searchBar">
          <input type="search" placeholder="Search by Title or Author" id="searchInput" v-model="searchQuery" @input="onInput" >
          <i class="fa-solid fa-magnifying-glass"></i>
      </div>
      </span>
      <i class="fa-solid fa-magnifying-glass mobile" @click="toggleSearchBar"></i>
  </template>
  
  <script>
  
  export default {
  name: 'SearchBar',
  data() {
      return {
          searchQuery: '',
          isSearchBarVisible: false,
          isDesktop: window.innerWidth > 760
      }
  },
  methods: {
      onInput() {
          this.$emit('search', this.searchQuery)
      },
      toggleSearchBar() {
      this.isSearchBarVisible = !this.isSearchBarVisible;
    },
  }
}
  </script>

<style>
.searchBar {
    background: #fffaf5;
    border-radius: 20px;
    height: 40px;
    width: 100%;
    padding-right: 30px;
    border: 1px solid #241400;

    display: flex;
    align-items: center;
    justify-content: space-between;
    
    overflow: hidden;
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
.mobile {
    display: none;
}

@media (max-width: 760px) {
    .searchBar {
        position: absolute;
        top: 80px;
        left: 0;
        right: 0;
        
        
        display: flex;
        align-items: center;
        margin: 0 auto;
        width: 90%;
        border: 1px solid #241400;
        transition: all 0.5s ease-in-out;
}
    .mobile {
        display: unset;
        cursor: pointer;
    }
}
</style>