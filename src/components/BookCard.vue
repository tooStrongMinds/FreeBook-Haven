<template>
  <div class="books">
    <div class="bookContainer" v-if="books.length">
          <a :href="book.amazon_product_url" v-for="book in books" :key="book.primary_isbn10" target="_blank">
            <div class="bookCard">
              <img :src="book.book_image" :alt="book.title">
              <div class="buttom">
                <span class="desc">
                  <h2>{{ book.title }}</h2>
                    <p>{{ book.author }}</p>
                </span>
                <button @click.prevent="toggleLibrary(book)"><i class="fa-regular fa-bookmark" v-if="!isFavorite(book)"></i>
                            <i class="fa-solid fa-bookmark" v-else></i></button>
              </div>
            </div>
          </a>
    </div>
    <h4 v-else>Loading Books...</h4>
  </div>
 
</template>

<script>
export default {
  name: 'BookCard',
  data() {
    return {
      // isFavorite: false
    }
  },
  props: {
    books: {
      type: Array,
      required: true
    },
    bookmarkedBooks: {
      type: Array,
      required: true
    }
    
  },
  methods: {
    toggleLibrary(book) {
      this.$emit('toggle-library', book);
    },
    isFavorite(book) {
      return this.bookmarkedBooks.some(b => b.primary_isbn10 === book.primary_isbn10);
      
    }
  }
}
</script>

<style scoped>
.books {
  margin-top: 30px;
}

.bookContainer {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  grid-gap: 20px;

  margin-top: 40px;
}
.bookCard {
  background: #fff;
  padding: 10px;
  border-radius: 10px;
  box-shadow: 6px 6px 8px #241400;

  

  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 10px;
  transition: transform 0.2s;
}

.buttom {
  display: flex;
  gap: 10px;
}

.bookCard:hover {
  transform: scale(1.02);
}

.bookCard img {
  height: auto;
  aspect-ratio: 3 / 4;
}
button {
  border: none;
  background: transparent;
  margin-right: 10px;
}
i {
  color: #e16a00;
  font-size: 20px;
}
a {
  text-decoration: none;
}
a .desc {
  display: flex;
  flex-direction: column;
  align-items: center;
  color: #000;
  padding-bottom: 10px;
  
}

h2 {
  font-size: 18px;
  height: 50px;
  margin-inline: 20px;

  align-content: center;
}
p {
  font-size: 15px;
  font-weight: 400;
}
</style>


