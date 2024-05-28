<template>
  <div class="wrapper">
    <SearchBar @search="performSearch"/>
    <div class="explore" v-if="isSearch">
      <h1>Your Search Results</h1>
      <BookCard :books="filteredBooks" :bookmarkedBooks="bookMarked" @toggle-library="toggleLibrary"/>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import BookCard from '@/components/BookCard.vue';
import SearchBar from '@/components/SearchBar.vue';

export default {
  components: { BookCard, SearchBar},
  data() {
    return {
      books: [],
      isSearch: false,
      filteredBooks: [],
      bookMarked: JSON.parse(localStorage.getItem('bookMarked')) || []
    }
  },
  mounted() {
    this.fetchData();
    
  },
  methods: {
    async fetchData() {
      try {
        const response = await axios.get('https://api.nytimes.com/svc/books/v3/lists/full-overview.json', {
          params: {
            'api-key': 'GkhC4ZLAXiOkazNFmMNAGzYHSWFIXaGR'
          }
        });

        // Assuming you want to display books from the first list in the results
        const lists = response.data.results.lists;
        if (lists.length > 0) {
          this.books = lists[0].books;
        } else {
          console.error('No lists found in the API response');
        }
      } catch (error) {
        console.error('Error fetching books:', error);
      }
    },
    performSearch(query) {
      if(query) {
        this.filteredBooks = this.books.filter(book =>
        book.title.toLowerCase().includes(query.toLowerCase()) ||
          (book.author && book.author.toLowerCase().includes(query.toLowerCase()))
        )
        this.isSearch = true
      } else {
        this.isSearch = false
      }
    },
    toggleLibrary(book) {
      const index = this.bookMarked.findIndex(b => b.primary_isbn10 === book.primary_isbn10);
      if (index > -1) {
        this.bookMarked.splice(index, 1);
      } else {
        this.bookMarked.push(book);
      }
      localStorage.setItem('bookMarked', JSON.stringify(this.bookMarked));
    },
    isFavorite(book) {
      return this.bookMarked.some(b => b.primary_isbn10 === book.primary_isbn10);
      
    }
  },
  // created() {
  //   this.$watch('bookMarked', () => {
  //     localStorage.setItem('bookMarked', JSON.stringify(this.bookMarked));
  //   }, { deep: true });
  // }
}
</script>