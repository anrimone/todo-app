<template>
  <div id="app">
    <todo-app></todo-app>
  </div>
  <div id="book">
    <quote-book></quote-book>
  </div>

</template>

<script>
import TodoApp from './components/TodoApp.vue'
import QuoteBook from './components/QuoteBook.vue'

export default {
  name: 'App',
  components: {
    TodoApp,
    QuoteBook
  }
}
</script>
