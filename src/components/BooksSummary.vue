<template>
  <div>
    <p>Total books: {{ booksLength }}</p>
    <p>Total price: {{ totalPrice }}</p>
  </div>
</template>

<script>
export default {
  name: 'BooksSummary',
  props: {
    books: {
      type: Array,
      required: true
    }
  },
  computed: {
    booksLength() {
      return this.books.length;
    },
    totalPrice() {
      return this.books.reduce((sum, book) => sum + book.price, 0);
    }
  }
}
</script>