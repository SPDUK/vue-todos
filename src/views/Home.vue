<template>
  <div class="home">
    <!-- todos refers to the todos returned from data(), passing down as todos as a prop -->
    <Todos v-bind:todos="todos" />
  </div>
</template>

<script>
import Todos from "../components/Todos";

export default {
  name: "home",
  components: { Todos },
  data() {
    return {
      todos: [
        {
          id: 1,
          title: "Todo One",
          completed: false
        },
        {
          id: 2,
          title: "Todo Two",
          completed: false
        },
        {
          id: 2,
          title: "Todo Three",
          completed: false
        }
      ]
    };
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