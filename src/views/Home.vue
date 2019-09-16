<template>
  <div class="home">
    <Todos />
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
  line-height: 14;
}
</style>