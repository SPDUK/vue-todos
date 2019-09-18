<template>
  <div class="home">
    <!-- todos refers to the todos returned from data(), passing down as todos as a prop -->
    <!-- catch the event with v-on  -->
    <Todos
      v-bind:todos="todos"
      v-on:handle-delete="handleDelete"
      v-on:handle-complete="handleComplete"
      v-on:handle-add-todo="addTodo"
    />
  </div>
</template>

<script>
import Todos from "../components/Todos";
import { update } from "ramda";

export default {
  name: "home",
  components: { Todos },
  data() {
    return {
      todos: JSON.parse(localStorage.getItem("todos")) || []
    };
  },
  methods: {
    saveTodos() {
      localStorage.setItem("todos", JSON.stringify(this.todos));
    },
    handleDelete(rowId) {
      const isNotRowId = ({ id }) => rowId !== id;
      this.todos = this.todos.filter(isNotRowId);

      this.$notify.success({
        title: "Success",
        message: "Deleted! 😎"
      });

      this.saveTodos();
    },
    handleComplete(rowId) {
      const idx = this.todos.findIndex(({ id }) => id === rowId);
      const currentTodo = this.todos[idx];

      const updatedTodo = {
        ...currentTodo,
        completed: !currentTodo.completed
      };

      // update todo state with new updated todo
      this.todos = update(idx, updatedTodo)(this.todos);

      // notify user of action working based on new completion status
      if (updatedTodo.completed) {
        this.$notify.success({
          title: "Success",
          message: `${updatedTodo.title} completed! 😎`
        });
      } else {
        this.$notify.info({
          title: "Info",
          message: `${updatedTodo.title} not completed! 😱`
        });
      }

      this.saveTodos();
    },
    addTodo(title) {
      // don't add empty todos
      if (title.length < 1) return;

      this.todos.push({
        id: Math.random(),
        title,
        completed: false
      });

      this.$notify.success({
        title: "Success",
        message: `${title} added!`
      });

      this.saveTodos();
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
}
</style>
