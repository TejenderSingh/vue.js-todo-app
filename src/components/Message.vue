<template>
  <b-message type="is-info" class="text-bold">{{message}}</b-message>
</template>

<script>
export default {
  name: "Message",
  props: {
    message: {
      type: String,
      required: true
    }
  }
};
</script>


<style scoped>
.text-bold {
  font-weight: bold;
}
</style>
