<template>
  <el-card class="box-card">
    <el-breadcrumb separator-class="el-icon-arrow-right">
      <el-breadcrumb-item :to="{ path: '/' }">首页</el-breadcrumb-item>
      <el-breadcrumb-item>活动管理</el-breadcrumb-item>
      <el-breadcrumb-item>活动列表</el-breadcrumb-item>
      <el-breadcrumb-item>活动详情</el-breadcrumb-item>
    </el-breadcrumb>
    <el-row class="mt20">
      <el-col :span="8">
        <el-input placeholder="请输入内容" v-model="query" clearable>
          <el-button slot="append" icon="el-icon-search"></el-button>
        </el-input>
      </el-col>
      <el-col :span="4">
        <el-button type="success" plain>添加用户</el-button>
      </el-col>
    </el-row>

    <el-table :data="usersData" style="width: 100%">
      <el-table-column type="index" label="#" width="180"></el-table-column>
      <el-table-column prop="username" label="姓名" width="180"></el-table-column>
      <el-table-column prop="email" label="邮箱"></el-table-column>
      <el-table-column prop="mobile" label="电话"></el-table-column>
      <el-table-column label="创建日期">
        <template slot-scope="usersData">{{usersData.row.create_time | fmtDate}}</template>
      </el-table-column>
      <el-table-column prop="mg_state" label="用户状态">
        <template>
          <el-switch :v-model="true" active-color="#13ce66" inactive-color="#ff4949"></el-switch>
        </template>
      </el-table-column>
      <el-table-column label="操作">
        <template>
          <el-button type="primary" icon="el-icon-edit" size="mini" circle plain></el-button>
          <el-button type="danger" icon="el-icon-delete" size="mini" circle plain></el-button>
          <el-button type="success" icon="el-icon-check" size="mini" circle plain></el-button>
        </template>
      </el-table-column>
    </el-table>
    <el-pagination
      @size-change="handleSizeChange"
      @current-change="handleCurrentChange"
      :current-page="pagenum"
      :page-sizes="[2, 4, 6, 8]"
      :page-size="2"
      layout="total, sizes, prev, pager, next, jumper"
      :total="total"
    ></el-pagination>
  </el-card>
</template>

<script>
export default {
  // create_time: 1486720211
  // email: "123@qq.com"
  // id: 502
  // mg_state: false
  // mobile: "120"
  // role_name: "测试角色2"
  // username: "linken"
  data() {
    return {
      query: "",
      usersData: [],
      pagenum: 1,
      pagesize: 2,
      total: -1
    };
  },
  created() {
    this.getUsersList();
  },
  methods: {
    // 分页功能
    handleSizeChange(val) {
      console.log(`每页 ${val} 条`);
      this.pagesize = val;
      this.pagenum = 1;
      this.getUsersList();
    },
    handleCurrentChange(val) {
      console.log(`当前页: ${val}`);
      this.pagenum = val;
      this.getUsersList();
    },
    async getUsersList() {
      const AUTH_TOKEN = localStorage.getItem("token");
      this.$http.defaults.headers.common["Authorization"] = AUTH_TOKEN;

      const res = await this.$http.get(
        `users?query=${this.query}&pagenum=${this.pagenum}&pagesize=${
          this.pagesize
        }`
      );
      console.log(res);
      const {
        data,
        meta: { msg, status }
      } = res.data;
      if (status === 200) {
        this.usersData = data.users;
        this.total = data.total;
        this.$message.success(msg);
      } else {
        this.$message.warning(msg);
      }
    }
  }
};
</script>

<style>
.mt20 {
  margin-top: 20px;
}
</style>
