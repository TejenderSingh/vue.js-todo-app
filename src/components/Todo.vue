<template>
  <section>
    <div class="item">
      <div class="item-children">
        <input type="checkbox" v-model="todo.completed">
        <p :class="{complete: todo.completed}">{{todo.title}}</p>
      </div>
      <button class="delete is-medium" @click="$emit('del-todo', todo.id)"></button>
    </div>
  </section>
</template>

<script>
export default {
  name: "Todo",
  props: {
    todo: {
      type: Object,
      required: true
    }
  }
};
</script>

<style scoped>
section {
  display: flex;
  justify-content: center;
  margin-bottom: 2px;
}
.item {
  width: 60%;
  max-width: 600px;
  background: #ecf0f1;
  padding: 10px;
  border-radius: 3px;
  display: flex;
  justify-content: space-between;
}
.item-children {
  display: flex;
  align-items: center;
}
.complete {
  text-decoration: line-through;
  color: gray;
}
.item-children input[type="checkbox"] {
  margin-right: 5px;
  cursor: pointer;
}
</style>
