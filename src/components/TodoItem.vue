<template>
  <li class="d-flex justify-content-between my-2">
    <span :class="{ completed : todo.completed }">
      <input type="checkbox" v-model="todo.completed" @click="compelteTodo" />
      <strong class="pl-2">{{ index + 1 }}</strong>
      {{ todo.title | uppercase }}
    </span>
    <button class="btn--remove" @click="removeTodo">D</button>
  </li>
</template>

<script>
export default {
  name: "TodoItem",
  props: {
    todo: {
      type: Object,
      required: true
    },
    index: Number
  },
  filters: {
    uppercase(value) {
      return value.toUpperCase();
    }
  },
  methods: {
    removeTodo() {
      this.$emit("removeTodo", this.todo.id);
    },
    compelteTodo() {
      this.todo.completed = !this.todo.completed;
    }
  }
};
</script>

<style>
.btn--remove {
  border-radius: 50px;
  background-color: red;
  border: none;
  outline: none;
}
.btn--remove:focus {
  outline: none;
}
li {
  cursor: pointer;
}
.completed {
  text-decoration: line-through;
}
</style>