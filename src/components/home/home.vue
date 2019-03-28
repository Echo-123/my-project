<template>
  <el-container class="container">
    <el-header class="header-wrap">
      <el-row>
        <el-col :span="8">
          <img src="../../assets/images/logo.png" alt>
        </el-col>
        <el-col :span="8">
          <div class="grid-content">后台管理系统</div>
        </el-col>
        <el-col :span="8" class="loginout-wrap">
          <a @click.prevent="loginOut()">退出</a>
        </el-col>
      </el-row>
    </el-header>
    <el-container>
      <el-aside class="aside" width="200px">
        <el-menu :router="true" class="el-menu-vertical-demo">
          <el-submenu index="1">
            <template slot="title">
              <i class="el-icon-location"></i>
              <span>用户管理</span>
            </template>
            <el-menu-item-group>
              <el-menu-item index="users">
                <i class="el-icon-location"></i>用户列表
              </el-menu-item>
            </el-menu-item-group>
          </el-submenu>
          <el-submenu index="2">
            <template slot="title">
              <i class="el-icon-menu"></i>
              <span>权限管理</span>
            </template>
            <el-menu-item-group>
              <el-menu-item index="1-1">
                <i class="el-icon-location"></i>角色列表
              </el-menu-item>
              <el-menu-item index="1-2">
                <i class="el-icon-location"></i>权限列表
              </el-menu-item>
            </el-menu-item-group>
          </el-submenu>
          <el-submenu index="3">
            <template slot="title">
              <i class="el-icon-location"></i>
              <span>商品管理</span>
            </template>
            <el-menu-item-group>
              <el-menu-item index="3-1">
                <i class="el-icon-location"></i>商品列表
              </el-menu-item>
              <el-menu-item index="3-2">
                <i class="el-icon-location"></i>分类参数
              </el-menu-item>
              <el-menu-item index="3-2">
                <i class="el-icon-location"></i>商品分类
              </el-menu-item>
            </el-menu-item-group>
          </el-submenu>
          <el-submenu index="4">
            <template slot="title">
              <i class="el-icon-setting"></i>
              <span>订单管理</span>
            </template>
            <el-menu-item-group>
              <el-menu-item index="1-1">
                <i class="el-icon-location"></i>订单列表
              </el-menu-item>
            </el-menu-item-group>
          </el-submenu>
          <el-submenu index="5">
            <template slot="title">
              <i class="el-icon-location"></i>
              <span>数据统计</span>
            </template>
            <el-menu-item-group>
              <el-menu-item index="1-1">
                <i class="el-icon-location"></i>数据报表
              </el-menu-item>
            </el-menu-item-group>
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
  // 在组件渲染之前 if token
  // 钩子函数在创建vm实例之前
  beforeCreate() {
    // 获取token
    const token = localStorage.getItem("token");
    if (!token) {
      this.$router.push({ name: "login" });
    }
  },
  methods: {
    loginOut() {
      this.$message.success("退出成功");
      localStorage.clear();
      this.$router.push({ name: "login" });
    }
  }
};
</script>

<style>
.container {
  height: 100%;
}
.el-header {
  height: 80px !important;
}
.header-wrap {
  background: #d11718;
}
.grid-content {
  text-align: center;
  color: #fff;
  font-size: 24px;
  line-height: 80px;
}
.loginout-wrap {
  text-align: right;
  color: #fff;
  line-height: 80px;
}
.loginout-wrap a {
  cursor: pointer;
}
.aside {
  background-color: #d3dce6;
}

.main {
  background-color: #e9eef3;
  height: 100%;
}
</style>
