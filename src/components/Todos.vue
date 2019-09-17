<template>
  <div class="container">
    <el-card class="box-card">
      <!-- filter out any todos that do not include the search state -->
      <!-- not sure how to put this inside a function yet outside the template, but you probably can -->
      <el-table
        :data="
          todos.filter(
            ({ title }) =>
              !search || title.toLowerCase().includes(search.toLowerCase())
          )
        "
      >
        <el-table-column label="Id" prop="id"></el-table-column>
        <el-table-column label="Title" prop="title"></el-table-column>
        <el-table-column align="right">
          <template slot="header">
            <el-input
              v-model="search"
              size="mini"
              placeholder="Type to search"
            />
          </template>
          <template slot-scope="scope">
            <el-button
              size="mini"
              type="danger"
              icon="el-icon-delete"
              circle
              @click="handleDelete(scope.$index, scope.row)"
            ></el-button>
            <el-button
              size="mini"
              icon="el-icon-edit"
              circle
              @click="handleEdit(scope.$index, scope.row)"
            ></el-button>
            <el-button
              size="mini"
              icon="el-icon-check"
              circle
              type="success"
              @click="handleComplete(scope.$index, scope.row)"
            ></el-button>
          </template>
        </el-table-column>
      </el-table>
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
      search: ""
    };
  },
  methods: {
    handleDelete(idx, row) {
      console.log(idx, row);
    },
    handleEdit(idx, row) {
      console.log(idx, row);
    },
    handleComplete(idx, row) {
      console.log(idx, row);
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
</style>
