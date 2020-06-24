<template>
  <form class="form-inline" @submit.prevent="addTodo">
    <div class="form-group mr-2 mb-2">
      <input type="text" v-model="title" class="form-control" placeholder="new TODO" />
    </div>
    <button type="submit" class="btn btn-primary mb-2">ADD</button>
  </form>
</template>

<script>
export default {
  name: "TodoItemCreator",
  data() {
    return {
      title: ""
    };
  },
  methods: {
    addTodo() {
			const todo = {
				id: Date.now(),
				title: this.title,
				completed: false
			}
			if(!this.title) return false;
			this.$emit('addTodo', todo)
      this.title = '';
    }
  }
};
</script>

<style>
</style>