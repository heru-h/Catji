<template>
  <div class="header-wrap">
    <div class="header">
      <ul class="nav">
        <li class="logo">
          <router-link to="/">
            <img height="75" src="../assets/logo_demo2_00.png" />
          </router-link>
        </li>
        <li v-if="!this.$store.state.user.hasOwnProperty('usid')">
          <router-link to="/login">登录</router-link>
        </li>
        <li v-if="!this.$store.state.user.hasOwnProperty('usid')">
          <router-link to="/register">注册</router-link>
        </li>
        <li v-if="this.$store.state.user.hasOwnProperty('usid')">
          <router-link to="/catspace">猫咪广场</router-link>
        </li>
        <li>
          <router-link to="/search">
            <font-awesome-icon :icon="['fas', 'search']" />
          </router-link>
        </li>
      </ul>
      <ul class="nav">
        <li>
          <router-link :to="(this.$store.state.user.hasOwnProperty('usid')?'/space':'/login')">
            <font-awesome-icon :icon="['fas', 'user']" />&nbsp;
            <template
              v-if="this.$store.state.user.hasOwnProperty('usid')"
            >{{this.$store.state.user.nickname}}</template>
          </router-link>
        </li>
        <li v-if="this.$store.state.user.hasOwnProperty('usid')">
          <router-link :to="{path:'/logout',query:{src:'/'}}">注销</router-link>
        </li>
        <!-- <li>
            <router-link to="/message">消息</router-link>
        </li>-->
        <li>
          <router-link to="/blog">动态</router-link>
        </li>
        <li>
          <router-link to="/space/favorite">收藏</router-link>
        </li>
        <li>
          <router-link to="/space/history">历史</router-link>
        </li>
        <li class="upload">
          <router-link to="/upload">投稿</router-link>
        </li>
      </ul>
    </div>
  </div>
</template>

<style scoped>
.logo {
  margin-top: 7px;
}

.header-wrap {
  background: #fff;
  box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.08);
}

.header {
  width: 1200px;
  margin: 0 auto;
  line-height: 30px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.header-wrap,
.header {
  height: 55px;
}

.nav {
  display: flex;
  align-items: center;
}

.nav li {
  padding-left: 10px;
  padding-right: 10px;
  text-align: center;
  font-size: 12pt;
  transition: all 0.3s;
}

.nav li a {
  color: #222;
  display: block;
}

.nav li a:hover {
  color: #fb7299;
}

.upload {
  line-height: 75px;
  background: #fb7299;
  border-radius: 0 0 15px 15px;
}

.upload a {
  color: #fff !important;
}
</style>