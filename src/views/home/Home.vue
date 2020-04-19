<template>
  <el-container class="container">
    <el-header class="header">
      <el-row>
        <el-col :span="16" class="headerlogo">
          <div class="grid-content bg-purple">
            <img
              style="width:400px;height: 30px"
              src="../../assets/img/top.png"
              alt="无法显示图片"
            />
          </div>
        </el-col>
        <el-col :span="8" class="rightsection">
          <div class="grid-content bg-purple-light">
            <span class="el-dropdown-link userinfo-inner">欢迎您，管理员</span>
            <span class="userinfo-inner" @click="signout">退出</span>
          </div>
        </el-col>
      </el-row>
    </el-header>
    <el-container>
      <el-aside class="aside">
        <!-- 侧边栏导航  -->
        <!-- unique-opened只展开一个 -->
        <!-- router开启路由模式 -->
        <el-menu :unique-opened="true" :router="true" class="menu"
          background-color=" #3A3A3A"
          text-color="#fff"
          active-text-color="#ffd04b"
          >
          <el-submenu :index="' '+item1.order" v-for="(item1,index) in menuData" :key="item1.path">
            <!--表示可以展开的一组 -->
            <template slot="title" @click="clickTitle">
              <!--图标 -->
              <i class="el-icon-location"></i>
              <!--文字 -->
              <span>{{item1.name}}</span>
            </template>
            <el-menu-item
              class="menuItem"
              @click="clickMenuItem"
              v-for="(item2,index) in item1.children"
              :key="item2.path"
              :index="item2.path"
            >
              <i class="el-icon-location"></i>
              <!--图标 -->
              <span>{{item2.name}}</span>
            </el-menu-item>
          </el-submenu>
        </el-menu>
      </el-aside>
      <el-main class="main">
        <!-- <manage-sys-home :style="style"></manage-sys-home> -->
        <!--首页信息 -->
        <router-view></router-view>
      </el-main>
    </el-container>
  </el-container>
</template>

<script>
// import ManageSysHome from "./childComponent/ManageSysHome";
export default {
  name: "Home",
  components: {
    // ManageSysHome,
  },
  data() {
    return {
      style: {
        display: "block",
      },
      menuData: [
        {
          name: "企业信息管理",
          order: "1",
          path:'componyinfomanage',
          children: [
            {
              path: "componyinfomanage",
              name: "企业信息",
            },
          ],
        },
        {
          path: "postinfomange",
          name: "岗位信息管理",
          order: "2",
          children: [
            {
              path: "postinfomange",
              name: "岗位信息",
            },
          ],
        },
        {
          path: "orderinfomange",
          name: "订单信息管理",
          order: "3",
          children: [
            {
              path: "orderinfomange",
              name: "订单信息",
            },
          ],
        },
        {
          path: "datamangeinfo",
          name: "数据字典",
          order: "4",
          children: [
            {
              path: "datamangeinfo",
              name: "岗位类型",
            },
          ],
        },
      ],
    };
  },
  methods: {
    //退出
    signout() {
      this.$confirm("退出登录, 是否继续?", "提示", {
        confirmButtonText: "确定",
        cancelButtonText: "取消",
        type: "warning",
      }).then(() => {
        this.$router.push({ path: "/" });
      });
    },
    clickMenuItem() {
      console.log("....");
      this.style.display = "none";
    },
    //回到首页
    clickTitle() {
      this.style.display = "block";
    },
  },
};
</script>
<style scoped>
.container {
  height: 100vh;
  font-size: 15px;
}
.header {
  background: #212121;
  color: #fff;
}
.aside {
  background: #3a3a3a;
  color: #fff;
  /* height: 100%; */
}
.menu {
  background: none;
  color: #fff;
}
.main {
  /* height: 100%; */
  color: #212121;
}
.headerlogo {
  line-height: 60px;
  margin-top: 10px;
}
.rightsection {
  line-height: 60px;
  text-align: center;
}
</style>
