<template>
  <div>
    <div v-bind:key="todo_aux.id" v-for="todo_aux in todolist">
      <TodoItem v-bind:todo="todo_aux" v-on:del-todo="$emit('del-todo',todo_aux.id)"/>
    </div>
  </div>
</template>

<script>
import TodoItem from "./TodoItem.vue";
export default {
  name: "TodoList",
  components: {
    TodoItem
  },
  props: ["todolist"]
};
</script>

<style scoped>
</style>
