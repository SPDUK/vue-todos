<template>
  <div class="container">
    <el-card class="box-card">
      <!-- filter out any todos that do not include the search state -->
      <el-table
        :data="todos.filter(({ title }) => !search || title.toLowerCase().includes(search.toLowerCase()))"
      >
        <el-table-column label="Id" prop="id"></el-table-column>
        <el-table-column label="Title" prop="title"></el-table-column>
        <el-checkbox>Completed?</el-checkbox>
        <el-table-column align="right">
          <template slot="header" slot-scope="scope">
            <el-input v-model="search" size="mini" placeholder="Type to search" />
          </template>
          <template slot-scope="scope">
            <el-button size="mini" @click="handleEdit(scope.$index, scope.row)">Edit</el-button>
            <el-button
              size="mini"
              type="danger"
              @click="handleDelete(scope.$index, scope.row)"
            >Delete</el-button>
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