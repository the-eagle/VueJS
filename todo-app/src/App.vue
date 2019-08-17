<template>
  <div>
    <Header />
    <AddTodo @add-todo="addTodo" />
    <Todos v-bind:todos="todos" @del-todo="deleteTodo" />
  </div>
</template>

<script>
import Todos from "./components/Todos.vue";
import AddTodo from "./components/AddTodo.vue";
import Header from "./components/Header.vue";
import axios from "axios";

export default {
  name: "todo-app",
  data() {
    return {
      todos: []
    };
  },
  methods: {
    deleteTodo(id) {
      axios
        .delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
        .then(
          reponse => (this.todos = this.todos.filter(todo => todo.id != id))
        )
        .catch();
    },
    addTodo(newTodo) {
      const { title, completed } = newTodo;
      axios
        .post("https://jsonplaceholder.typicode.com/todos", {
          title,
          completed
        })
        .then(reponse => this.todos.push(reponse.data))
        .catch(err => console.log(err));
    }
  },
  components: {
    Todos,
    AddTodo,
    Header
  },
  created() {
    axios
      .get("https://jsonplaceholder.typicode.com/todos?_limit=6")
      .then(response => (this.todos = response.data))
      .catch(err => console.log(err));
  }
};
</script>

<style>
</style>