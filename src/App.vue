<template>
  <div id="app">
    <Header/>
    <AddTodo v-on:add-todo="addTodo"/>
    <TodoList v-bind:todolist="todolist_app" v-on:del-todo="deleteTodo"/>
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import TodoList from "./components/TodoList";
import AddTodo from "./components/AddTodo";

export default {
  name: "app",
  components: {
    Header,
    AddTodo,
    TodoList
  },
  data() {
    return {
      todolist_app: [
        {
          id: 1,
          title: "Item 1",
          completed: false
        },
        {
          id: 2,
          title: "Item 2",
          completed: false
        }
      ]
    };
  },
  methods: {
    deleteTodo(id) {
      this.todolist_app = this.todolist_app.filter(todo => todo.id != id);
    },
    addTodo(newTodo) {
      this.todolist_app = [...this.todolist_app, newTodo];
    }
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
