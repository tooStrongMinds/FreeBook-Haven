<template>
    <div class="library">
      <h2>Your Library</h2>
      
      <BookCard :books="libraryBooks" :bookmarkedBooks="libraryBooks" @toggle-library="removeFromLibrary"/>
    </div>
  </template>
  
  <script>
import BookCard from '@/components/BookCard.vue';

  export default {
    components:{BookCard},
    data() {
      return {
        libraryBooks: JSON.parse(localStorage.getItem('bookMarked')) || []
      }
    },
    methods: {
    removeFromLibrary(book) {
      const index = this.libraryBooks.findIndex(b => b.primary_isbn10 === book.primary_isbn10);
      if (index > -1) {
        this.libraryBooks.splice(index, 1);
        localStorage.setItem('bookMarked', JSON.stringify(this.libraryBooks));
      }
    }
  }
  }
  </script>
  

<style>

</style>