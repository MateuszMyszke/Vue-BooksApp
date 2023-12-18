<template>
  <div id="app" class="app" >

    <!-- heading -->
    <header class="app__heading">
      <h1>Books<span>.app</span></h1>
    </header>

    <!-- books list -->
    <books-list 
      @remove="removeBook"
      :books="books" />

    <!-- no books message -->
    <booksLengthMsg 
      :booksLength="books.length" />

    <!-- add book form -->
    <bookForm @add="addBook" />

    <booksSummary :books="books"/>
  </div>
</template>

<script>
import BooksLengthMsg from './components/BooksLengthMsg.vue'
import BooksList from './components/BooksList.vue'
import BookForm from './components/BookForm.vue'
import BooksSummary from './components/BooksSummary.vue'

export default {
  name: 'App',
  data: () => ({
    books: [],
    form: {
    title: '',
    price: 0
    }
  }),
  methods: {
    removeBook (index) {
      this.books.splice(index, 1)
    },
    addBook (book) {
      this.books.push({ ...book })
    }
  },
  components: { BooksList, BooksLengthMsg, BookForm, BooksSummary },
  mounted() {
    this.fetchBooks();
  },
  methods: {
    async fetchBooks() {
      try {
        const response = await fetch('https://api.itbook.store/1.0/new');
        const data = await response.json();
        const formattedBooks = data.books.slice(0, 3).map(book => ({
          title: book.title,
          price: parseFloat(book.price.replace('$', '')), 
        }));
        this.books = formattedBooks;
      } catch (error) {
        console.error('Error fetching books:', error);
      }
    },
  },
}
</script>

<style lang="scss" scoped>
.app {
  width: 100%;
  max-width: 1000px;
  padding: 2rem;
  margin: 0 auto;

  &__heading {
    font-size: 3rem;
    text-align: center;
    span {
      color: #5a58da;
    }
  }
}
</style>