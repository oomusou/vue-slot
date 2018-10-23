<template>
  <div id="todo-list">
    <input type="text" v-model="input">
    <button @click="addItem">Add</button>
    <ul>
      <li v-for="(todo, index) in todos" @click="finishItem(index)" :key="index">
        <slot :todo="todo">
          {{ todo.title }}
        </slot>
      </li>
    </ul>
  </div>
</template>

<script>
const finishItem = function(index) {
  this.todos[index].completed = !this.todos[index].completed;
};

const addItem = function() {
  const elem = {
    title: this.input,
    completed: false,
  };
  this.todos = [...this.todos, elem];
};

const source = function(value) {
  this.todos = value;
};

const props = [
  'source',
];

const data = function() {
  return {
    input: '',
    todos: [],
  };
};

const watch = {
  source,
};

const methods = {
  finishItem,
  addItem,
};

export default {
  name: 'todo-list',
  props,
  data,
  watch,
  methods,
};
</script>

<style scoped>

</style>
