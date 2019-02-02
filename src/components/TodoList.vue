<template>
  <div>
    <div v-for="todo in todos" :key="todo.id">
      <Todo :todo="todo" v-on:del-todo="$emit('delete-todo', todo.id)"/>
    </div>
  </div>
</template>

<script>
import Todo from "./Todo.vue";
export default {
  name: "TodoList",
  components: {
    Todo
  },
  props: {
    todos: {
      type: Array,
      required: true
    }
  }
};
</script>

<style scoped>
</style>

