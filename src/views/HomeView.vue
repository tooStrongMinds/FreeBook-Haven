<template>
  <div class="home wrapper">
    <div class="headContent">
      <span class="text">
        <h1>FreeBook Haven</h1>
        <p>
          Welcome to FreeBook Haven, your ultimate destination for discovering and downloading free e-books. Whether you're into fiction, non-fiction, or self-help, we've got something for every reader. Dive into our extensive collection, find hidden gems, and enjoy reading without any cost. Start your literary adventure today!
        </p>
      </span>
      <img :src="headerImg">
    </div>
    <h1>Recommended Books</h1>
    <BookCard :books="books" :bookmarkedBooks="bookMarked" @toggle-library="toggleLibrary"/>
  </div>
</template>

<script>
import axios from 'axios';
import BookCard from '@/components/BookCard.vue';

export default {
  components: { BookCard},
  data() {
    return {
      headerImg: require('@/assets/HeaderImg.png'),
      books: [],
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
    toggleLibrary(book) {
      const index = this.bookMarked.findIndex(b => b.primary_isbn10 === book.primary_isbn10);
      if (index > -1) {
        this.bookMarked.splice(index, 1);
        alert(`${book.title} has been removed from your library`);
      } else {
        this.bookMarked.push(book);
        alert(`${book.title} has been added to your library`);
      }
      localStorage.setItem('bookMarked', JSON.stringify(this.bookMarked));
    },
    isFavorite(book) {
      return this.bookMarked.some(b => b.primary_isbn10 === book.primary_isbn10);

    }
  }
}
</script>

<style scoped>
.headContent {
  display: flex;
  align-items: center;
  gap: 20px;
}

img {
  width: 500px;
}

h1 {
  font-size: 45px;
  font-weight: 900;
}
h1:nth-child(2) {
  font-family: 'Jost', sans-serif;
  color: #241400;
  font-size: 32px;
}

p {
  font-size: 20px;
  font-weight: 500;
  text-align: left;
}

.text {
  width: 90%;
  display: flex;
  flex-direction: column;
  gap: 20px;
}
@media (max-width: 760px) {
  .headContent {
    display: block;;
  }
}
</style>
