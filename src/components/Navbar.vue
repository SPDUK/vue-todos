<template>
  <el-menu
    :default-active="$route.path"
    class="el-menu"
    mode="horizontal"
    router
  >
    <el-menu-item index="/">
      <router-link to="/">
        Home
      </router-link>
    </el-menu-item>
    <el-menu-item index="/about">
      <router-link to="/about">
        About
      </router-link>
    </el-menu-item>
    <el-menu-item @click="visitGithub">
      <a href="#"> Github</a>
    </el-menu-item>
  </el-menu>
</template>

<script>
export default {
  methods: {
    visitGithub() {
      window.open("https://github.com/SPDUK/vue-todos", "_blank");
    }
  }
};
</script>

<style scoped>
.el-menu {
  margin-bottom: 60px;
}
</style>
