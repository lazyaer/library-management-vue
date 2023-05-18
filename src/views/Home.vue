<template>
  <div>
    <!-- 搜索表单   -->
    <div style="margin-bottom: 20px">
      <el-input placeholder="请输入姓名" style="width: 240px" v-model="params.name"/>
      <el-input placeholder="请输入联系方式" style="width: 240px;margin-left: 5px" v-model="params.phone"/>
      <el-button type="primary" icon="el-icon-search" @click="load">搜索</el-button>
      <el-button type="warning" icon="el-icon-refresh" @click="reset">重置</el-button>

    </div>

    <el-table :data="tableData" stripe>
      <el-table-column prop="name" label="姓名"></el-table-column>
      <el-table-column prop="username" label="用户名"></el-table-column>
      <el-table-column prop="gender" label="性别"></el-table-column>
      <el-table-column prop="age" label="年龄"></el-table-column>
      <el-table-column prop="phone" label="联系方式"></el-table-column>
      <el-table-column prop="address" label="地址"></el-table-column>
    </el-table>

    <!--  分页  -->
    <div class="block">
      <el-pagination
          background
          @size-change="handleSizeChange"
          @current-change="handleCurrentChange"
          :page-sizes="[5, 10, 20]"
          :current-page="params.pageNum"
          :page-size="params.pageSize"
          layout="total, sizes, prev, pager, next, jumper"
          :total="total">
      </el-pagination>
    </div>
  </div>
</template>

<script>
import request from "@/utils/request";

export default {
  name: "Home",
  data(){
    return{
      tableData:[],
      total: 10,
      params:{
        pageSize: 10,
        pageNum: 1,
        name: '',
        phone: ''
      }
    }
  },
  created(){
    this.load()
  },
  methods:{
    // 重置所有
    reset(){
      this.params = {}
      this.load()
    },
    load(){
      request.get("/user/page",{
        params: this.params
      }).then(res =>{
        this.tableData = res.data.records
        this.total = res.data.total
      })
    },
    // 改变当前每页的个数触发
    handleSizeChange(pageSize){
      this.params.pageSize = pageSize
      this.load()
    },
    // 改变当前页码出发
    handleCurrentChange(pageNum){
      this.params.pageNum = pageNum
      this.load()
    },
  }
}
</script>

<style scoped>

</style>