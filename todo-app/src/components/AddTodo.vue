<template>
  <div>
    <form @submit.prevent="createTodo">
      <input v-model="title" type="text" placeholder="Add a Todo ..." />
      <input type="submit" value="Add To List" />
    </form>
  </div>
</template>

<script>

export default {
  name: "AddTodo",
  data() {
    return {
      title: ""
    };
  },
  methods: {
    createTodo() {
      const newTodo = {
        title: this.title,
        completed: false
      };
      this.title = "";
      this.$emit("add-todo", newTodo);
    }
  }
};
</script>

<style scoped>
form {
  display: flex;
}
input[type="text"] {
  flex: 10;
  padding: 5px;
}
imput[type="submit"] {
  flex: 2;
}
</style>