<template>
  <nav>
    <img :src="logo" alt="Site Logo" class="logo" />
    <SearchBar @search="performSearch"/>
    <NavBar />
  </nav>
  <router-view/>
</template>

<script>
import NavBar from '@/components/NavBar.vue'
import SearchBar from '@/components/SearchBar.vue'

export default {
  data() {
    return {
      logo: require('@/assets/Group.png')
    }
  },
  components: {
    NavBar, SearchBar
  }
}
</script>

<style>
#app {
  font-family: 'Montserrat', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #000;
}
</style>
