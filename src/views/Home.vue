<template>
  <div id="app">
    <AddTodo v-on:add-todo="addTodo"/>
    <TodoList v-bind:todolist="todolist_app" v-on:del-todo="deleteTodo"/>
  </div>
</template>

<script>
import TodoList from "../components/TodoList";
import AddTodo from "../components/AddTodo";
import axios from "axios";

export default {
  name: "Home",
  components: {
    AddTodo,
    TodoList
  },
  data() {
    return {
      todolist_app: []
    };
  },
  methods: {
    deleteTodo(id) {
      axios
        .delete(`http://jsonplaceholder.typicode.com/todos/${id}`)
        .then(
          resp =>
            (this.todolist_app = this.todolist_app.filter(
              todo => todo.id != id
            ))
        )
        .catch(err => console.log(err));
    },
    addTodo(newTodo) {
      const { title, completed } = newTodo;

      axios
        .post("http://jsonplaceholder.typicode.com/todos", {
          title,
          completed
        })
        .then(resp => (this.todolist_app = [...this.todolist_app, resp.data]))
        .catch(err => console.log(err));
    }
  },
  created() {
    axios
      .get("http://jsonplaceholder.typicode.com/todos?_limit=10")
      .then(response => (this.todolist_app = response.data))
      .catch(err => console.log(err));
  }
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.4;
}

.btn {
  display: inline-blok;
  border: none;
  background: #555;
  color: #ffffff;
  padding: 7px 20px;
  cursor: pointer;
}

.btn:hover {
  background: #666;
}
</style>
