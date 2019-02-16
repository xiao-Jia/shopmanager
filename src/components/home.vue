<template>
  <el-container class="container">
    <el-header>
      <el-row>
        <el-col :span="4">
            <img src="@/assets/logo.png" alt="图片加载失败">
        </el-col>
        <el-col class="middle" :span="19">
            <h2>电商后台管理系统</h2>
        </el-col>
        <el-col :span="1">
            <a class="logout" href="#">退出</a>
        </el-col>
      </el-row>
    </el-header>
    <el-container>
      <el-aside class="aside" width="200px">Aside</el-aside>
      <el-main class="main">Main</el-main>
    </el-container>
  </el-container>
</template>

<script>
export default {};
</script>

<style>
.container {
  background-color: #B3C0D1;
  height: 100%;
}
.aside {
  background-color: skyblue;
}
.main {
  background-color: gold;
}
.middle{
    text-align: center;
    line-height: 60px;
    color: #fff;
}
.logout{
    text-align: center;
    line-height: 60px;
}
</style>
