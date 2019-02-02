<template>
  <form @submit.prevent="addTodo">
    <section>
      <b-field grouped position="is-centered" class="formStyle">
        <b-input size="is-medium" v-model="title" rounded placeholder="What needs to be done?"></b-input>
        <p class="control mt">
          <button class="button is-primary is-medium is-rounded is-outlined">Add Todo</button>
        </p>
      </b-field>
    </section>
  </form>
</template>

<script>
import shortid from "shortid";
export default {
  name: "TodoForm",
  data() {
    return {
      title: ""
    };
  },
  methods: {
    addTodo() {
      const newTodo = {
        id: shortid.generate(),
        title: this.title,
        completed: false
      };
      this.$emit("add-todo", newTodo);
      this.title = "";
    }
  }
};
</script>

<style scoped>
section {
  margin: 3rem 0;
}
@media screen and (max-width: 420px) {
  .formStyle {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  .mt {
    margin-top: 1rem;
  }
}
</style>

