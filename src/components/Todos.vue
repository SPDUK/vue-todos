<template>
  <div class="container">
    <el-card class="box-card">
      <!-- filter out any todos that do not include the search state -->
      <!-- not sure how to put this inside a function yet outside the template, but you probably can -->
      <el-table
        class="table"
        :row-class-name="tableRowClassName"
        :data="
          todos.filter(
            ({ title }) =>
              !search || title.toLowerCase().includes(search.toLowerCase())
          )
        "
      >
        >
        <el-table-column label="Title" prop="title"></el-table-column>
        <el-table-column align="right">
          <template slot="header" slot-scope="scope">
            <el-input
              v-model="search"
              size="mini"
              placeholder="Type to search"
            />
          </template>
          <template slot-scope="scope">
            <!-- emit an event up to the Home component -->
            <el-button
              size="mini"
              type="danger"
              icon="el-icon-delete"
              circle
              @click="$emit('handle-delete', scope.row.id)"
            ></el-button>
            <el-button
              size="mini"
              icon="el-icon-check"
              circle
              type="success"
              @click="$emit('handle-complete', scope.row.id)"
            ></el-button>
          </template>
        </el-table-column>
      </el-table>
      <form @submit="handleSubmit" class="add-todo">
        <el-input
          class="add-todo-input"
          placeholder="Create a new todo..."
          v-model="input"
          autofocus="true"
        ></el-input>
        <el-button class="add-todo-button" type="primary" native-type="submit"
          >Add Todo</el-button
        >
      </form>
    </el-card>
  </div>
</template>

<script>
export default {
  // component name
  name: "Todos",
  // like prop types in react, but also makes the prop available(?)
  props: {
    todos: Array
  },
  data() {
    return {
      search: "",
      input: ""
    };
  },
  methods: {
    tableRowClassName: ({ row: { completed } }) =>
      completed ? "completed-row" : "",
    handleSubmit(e) {
      e.preventDefault();
      this.$emit("handle-add-todo", this.input);
      this.input = "";
    }
  }
};
</script>

<style scoped>
.container {
  display: flex;
  justify-content: center;
}
.box-card {
  width: 95%;
  max-width: 800px;
}

.table {
  max-height: 60vh;
  overflow: auto;
}
.add-todo {
  margin-top: 20px;
  display: flex;
  justify-content: space-between;
}
.add-todo-input {
  margin-right: 20px;
  max-width: 70%;
}
.add-todo-button {
  width: 105px;
  margin-right: 10px;
}
</style>

<style>
.el-table .completed-row {
  background: #f0f9eb;
  text-decoration: line-through;
}
</style>
