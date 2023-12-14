<template>
  <div id="app">

    <!-- heading -->
    <header>
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

  </div>
</template>

<script>
import BooksLengthMsg from './components/BooksLengthMsg.vue'
import BooksList from './components/BooksList.vue'
import BookForm from './components/BookForm.vue'

export default {
  name: 'App',
  data: () => ({
    books: [
      {
        title: 'The Catcher in the Rye',
        price: 20
      },
      {
        title: 'Of Mice and Men',
        price: 18
      }
    ],
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
  components: { BooksList, BooksLengthMsg, BookForm }
}
</script>