<template>
  <form @submit.prevent="addTodo">
    <section>
      <b-field grouped position="is-centered" class="formStyle">
        <b-input size="is-medium" v-model="title" rounded placeholder="What needs to be done?"></b-input>
        <p class="control mt">
          <input
            type="submit"
            value="Add Todo"
            class="button is-primary is-medium is-rounded is-outlined"
          >
        </p>
      </b-field>
      <div class="errors" v-for="(error, index) in errors" :key="index">{{ error }}</div>
    </section>
  </form>
</template>

<script>
import shortid from "shortid";
export default {
  name: "TodoForm",
  data() {
    return {
      title: "",
      errors: []
    };
  },
  methods: {
    addTodo() {
      this.errors = [];
      if (!this.title) {
        this.errors.push("Please enter some text");
      }
      if (!this.errors.length) {
        const newTodo = {
          id: shortid.generate(),
          title: this.title,
          completed: false
        };
        this.$emit("add-todo", newTodo);
        this.title = "";
        this.errors = [];
      }
    }
  }
};
</script>

<style scoped>
section {
  margin: 3rem 0;
}
.errors {
  display: flex;
  justify-content: center;
  color: red;
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

