<template>
  <div id="app">
    <todo-list></todo-list>
  </div>
</template>

<script>
import todoList from './components/TodoList'

export default {
  name: 'App',
  components: {
      todoList
  }
}
</script>

