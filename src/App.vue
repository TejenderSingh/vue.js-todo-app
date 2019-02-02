<template>
  <div id="app">
    <Header/>
    <Message v-if="todosLengthNotZero" :message="'Todos left: ' + todosLeft"/>
    <Message v-else message="Add some todos"/>
    <div class="container">
      <TodoForm v-on:add-todo="handleAddTodo"/>
      <TodoList :todos="filteredTodos" v-on:delete-todo="handleDelete"/>
      <div v-show="todosLengthNotZero" class="set-width mt10">
        <label class="checkbox">
          <input type="checkbox" :checked="!todosLeft" @change="handleCheckAll">
          {{todosLeft ? "Check all" : "Uncheck all"}}
        </label>
      </div>
      <div v-show="todosLengthNotZero" class="buttons has-addons is-centered mt30">
        <button class="button is-primary is-active" @click="todosToShow = 'all'">All</button>
        <button class="button is-info" @click="todosToShow = 'active'">Active</button>
        <button class="button is-success" @click="todosToShow = 'completed'">Completed</button>
      </div>
      <div v-show="someTodosCompleted" class="buttons is-centered">
        <button class="button is-danger" @click="handleRemoveAllCompleted">Remove all completed</button>
      </div>
    </div>
  </div>
</template>

<script>
import TodoForm from "./components/TodoForm.vue";
import Header from "./components/Header.vue";
import Message from "./components/Message.vue";
import TodoList from "./components/TodoList.vue";

export default {
  name: "app",
  components: {
    TodoForm,
    Header,
    Message,
    TodoList
  },
  data() {
    return {
      todos: [
        { id: 1, title: "Buy grocery", completed: false },
        { id: 2, title: "Redesign website", completed: true },
        { id: 3, title: "Walk the dog", completed: false }
      ],
      todosToShow: "all"
    };
  },
  computed: {
    todosLeft() {
      return this.todos.filter(todo => !todo.completed).length;
    },
    todosLengthNotZero() {
      return this.todos.length;
    },
    someTodosCompleted() {
      return this.todos.some(todo => todo.completed);
    },
    filteredTodos() {
      if (this.todosToShow == "all") {
        return this.todos;
      } else if (this.todosToShow == "active") {
        return this.todos.filter(todo => !todo.completed);
      } else if (this.todosToShow == "completed") {
        return this.todos.filter(todo => todo.completed);
      }
      return this.todos;
    }
  },
  methods: {
    handleAddTodo(todo) {
      this.todos = [...this.todos, todo];
    },
    handleDelete(id) {
      this.todos = this.todos.filter(todo => todo.id !== id);
    },
    handleCheckAll(e) {
      this.todos.map(todo => (todo.completed = e.target.checked));
    },
    handleRemoveAllCompleted() {
      this.todos = this.todos.filter(todo => !todo.completed);
    }
  }
};
</script>

<style>
html {
  margin: 0;
  padding: 0;
  height: 100vh;
}
body {
  min-height: 100%;
}
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

.set-width {
  margin: 0 auto;
  width: 60%;
  max-width: 600px;
}
.set-width input[type="checkbox"] {
  margin-left: 10px;
  cursor: pointer;
}
.mt10 {
  margin-top: 10px;
}
.mt30 {
  margin-top: 30px;
}
</style>
