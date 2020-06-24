<template>
  <div>
    <router-link to="/">To Home</router-link>
    <TodoList />
  </div>
</template>

<script>
import TodoList from "../components/TodoList.vue";

export default {
  name: "App",
  components: {
    TodoList
  }
};
</script>
