<template>
  <div id="app">
    <!--  头部区域  -->
    <div style="height: 60px;line-height:60px;background-color:white;margin-bottom:2px;">
      <img src="@/assets/logo.png" alt="" style="width: 60px; position: relative;left: 20px">
      <span style="margin-left: 35px; font-size: 24px;position: absolute;">图书管理系统</span>
    </div>

    <!--  侧边栏和主体  -->
    <div style="display: flex">
      <!-- 侧边栏导航 -->
      <div style="min-height: calc(100vh - 62px);width:200px;overflow: hidden; margin-right: 2px;background-color: white">
        <el-menu :default-active="$router.path" :default-openeds="['/']" router class="el-menu-demo">
          <el-menu-item index="/">
            <i class="el-icon-s-home"></i>
            <span>首页</span>
          </el-menu-item>
          <el-submenu index="/">
            <template slot="title">
              <i class="el-icon-user-solid"/>
              <span>会员管理</span>
            </template>
            <el-menu-item index="user">会员列表</el-menu-item>
            <el-menu-item index="addUser">添加会员</el-menu-item>
          </el-submenu>
        </el-menu>
      </div>
      <!-- 主体数据   -->
      <div style="flex: 1;background-color: white;padding: 10px">
        <router-view/>
      </div>
    </div>
  </div>
</template>
