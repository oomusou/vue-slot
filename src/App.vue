<template>
  <div id="app">
    <todo-list :source="todos">
      <template slot-scope="{ todo }">
        <span v-if="todo.completed">✓</span>
        {{ todo.title }}
      </template>
    </todo-list>
  </div>
</template>

<script>
import TodoList from './components/todo-list.vue';
import { fetchTodos } from './api/todos.api';

const mounted = function() {
  const response = res =>
    this.todos = res.data.slice(0, 5);

  fetchTodos()
    .then(response);
};

const components = {
  TodoList,
};

const data = function() {
  return {
    todos: [],
  };
};

export default {
  name: 'app',
  components,
  data,
  mounted,
};
</script>

<style>
</style>
