<template>
  <div class="container w-75">
    <TodoItemCreator @addTodo="addTodo" />
    <select v-model="filter">
      <option value="all">All</option>
      <option value="completed">Completed</option>
      <option value="not-completed">Not Completed</option>
    </select>
    <Loader v-if="loading" />
    <ul class="p-0" v-else-if="filteredTodos.length">
      <TodoItem
        v-for="(todo,i) in filteredTodos"
        :index="i"
        :key="todo.id"
        :todo="todo"
        @removeTodo="removeTodo"
      />
    </ul>
    <p v-else>Todos not found</p>
  </div>
</template>

<script>
import TodoItem from "./TodoItem";
import TodoItemCreator from "./TodoItemCreator";
import Loader from "./Loader";

export default {
  name: "TodoList",
  data() {
    return {
      todos: [],
      loading: false,
      filter: "all"
    };
  },
  components: {
    TodoItem,
    TodoItemCreator,
    Loader
  },
  computed: {
    filteredTodos() {
      if (this.filter === "not-completed")
        return this.todos.filter(t => !t.completed);
      if (this.filter === "completed")
        return this.todos.filter(t => t.completed);
      return this.todos;
    }
  },
  async mounted() {
    this.loading = true;
    await fetch("https://jsonplaceholder.typicode.com/todos?_limit=10")
      .then(response => response.json())
      .then(json => (this.todos = json));
    this.loading = false;
  },
  methods: {
    addTodo(todo) {
      this.todos.push(todo);
    },
    removeTodo(id) {
      this.todos = this.todos.filter(todo => todo.id !== id);
    }
  }
};
</script>

<style>
</style>