<template>
  <div>
    <div v-if="booksLength > 5">
      <p>{{ booksLength }} books</p>
    </div>
    <div v-else-if="booksLength > 1">
      <p>Not too many of them…</p>
    </div>
    <div v-else-if="booksLength === 1">
      <p>One single book!</p>
    </div>
    <div v-else>
      <p>Go get some books!</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'BooksLengthMsg',
  props: {
    booksLength: {
      type: Number,
      required: true
    }
  }
}
</script>
  