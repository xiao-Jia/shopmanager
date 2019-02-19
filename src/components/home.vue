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
          <a class="logout" href="#" @click="handleLoginout()">退出</a>
        </el-col>
      </el-row>
    </el-header>
    <el-container>
      <el-aside class="aside" width="200px">
        <el-menu
          :unique-opened="true"
          :router="true"
          default-active="2"
          class="el-menu-vertical-demo"
        >
          <el-submenu :index="item1.order+''" v-for="(item1) in menus" :key="item1.id">
            <template slot="title">
              <i class="el-icon-location"></i>
              <span>{{item1.authName}}</span>
            </template>
            <el-menu-item :index="item2.path+''" v-for="(item2) in item1.children" :key="item2.id">
              <i class="el-icon-menu"></i>
              <span>{{item2.authName}}</span>
            </el-menu-item>
          </el-submenu>
        </el-menu>
      </el-aside>
      <el-main class="main">
        <router-view></router-view>
      </el-main>
    </el-container>
  </el-container>
</template>

<script>
export default {
  data() {
    return {
      menus: []
    };
  },
  beforeMount() {
    
  },
  created() {
    this.getMenus();
  },
  methods: {
    //动态导航（侧边栏）
    async getMenus() {
      const res = await this.$http.get(`menus`);
      // console.log(res);
      const {
        meta: { msg, status },
        data
      } = res.data;
      if (status === 200) {
        this.menus = data;
      }
    },
    // 退出功能
    handleLoginout() {
      localStorage.clear();
      this.$router.push({
        name: "login"
      });
      this.$message.success("退出成功");
    }
  }
};
</script>

<style>
.container {
  background-color: #b3c0d1;
  height: 100%;
}
.aside {
  background-color: skyblue;
}
.main {
  background-color: gold;
}
.middle {
  text-align: center;
  line-height: 60px;
  color: #fff;
}
.logout {
  text-align: center;
  line-height: 60px;
}
</style>
