<template>
  <div class="registerr">
    <h1>Catji——同济猫咪分享社区</h1>
    <div class="container clearfix">
      <div class="login">
        <h2>登 录</h2>
        <div class="send-button">
          <router-link to="/login" class="some-class">
            <span>立即登录</span>
          </router-link>
        </div>
      </div>
      <div class="register">
        <h2>注 册</h2>
        <input type="text" placeholder="请输入用户名" v-model="nickname" :class="{on:usernameNotOk}" />
        <input type="text" placeholder="请输入邮箱" v-model="email" :class="{on:emailNotOk}" />
        <input type="password" placeholder="请输入密码" v-model="password1" />
        <input type="password" placeholder="再次输入以确认密码" v-model="password2" />
        <div class="send-button">
          <input type="button" value="注册" @click="onRegister()" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { register } from "@/api";
export default {
  name: "Registerr",
  data() {
    return {
      nickname: "",
      email: "",
      password1: "",
      password2: "",
      usernameNotOk: false,
      emailNotOk: false,
    };
  },
  methods: {
    async onRegister() {
      var password1 = this.password1.trim(),
        password2 = this.password2.trim(),
        nickname = this.nickname.trim(),
        email = this.email.trim();
      if (!nickname) {
        this.$message.error("用户名不能为空");
        return;
      }
      if (!email) {
        this.$message.error("邮箱地址不能为空");
        return;
      }

      var pattern = /^([a-zA-Z0-9])(\w|-)+@[a-zA-Z0-9]+\.([a-zA-Z]{2,4})$/;
      if (!pattern.test(this.email)) {
        this.$message.error("请检查邮箱格式");
        return;
      }
      if (!password1) {
        this.$message.error("密码不能为空");
        return;
      }
      if (password1 !== password2) {
        this.$message.error("两次输入的密码不一致");
        return;
      }
      try {
        let res = await register(nickname, email, "", password1);
        res = res.data;
        if (res.status === "ok") {
          let usid = res.data.usid;
          this.$store.commit("login", {
            usid,
            nickname,
            follower_num: 0,
            followee_num: 0,
            upload_num: 0,
          });
          this.$router.push({ path: "/" });
        } else {
          this.$message.error("网络错误: " + res.status);
        }
      } catch (e) {
        let res = e.response.data;
        this.$message.error("网络错误: " + res.status);
      }
    },
  },
};
</script>

<style scoped>
.some-class {
  text-align: center;
  display: block;
  width: 60%;
  padding: 10px 0;
  font-size: 16px;
  font-weight: 100;
  background-color: transparent;
  color: #ccc;
  border: 1px solid rgba(238, 238, 238, 0.41);
  border-width: thin;
  cursor: pointer;
  outline: none;
  transition: 0.5s all;
  text-decoration: none;
  margin-bottom: 20px;
}

.some-class:hover {
  background-color: rgb(0, 0, 0);
  border: 1px solid #fff;
  color: #fff;
  transition: 0.5s all;
  text-decoration: none;
}

.loginn {
  height: 1000px;
  font-family: "Roboto", sans-serif;
  text-align: center;
  background: url("../assets/backgroundd.jpg");
  background-repeat: no-repeat;
  background-attachment: fixed;
  background-position: center;
  background-size: cover;
}

body a {
  transition: 0.5s all;
  text-decoration: none;
}

h1 {
  font-size: 45px;
  font-weight: 500;
  /* height: 400px; */
  line-height: 200px;
  letter-spacing: 4px;
  color: #ffffff;
}

.container {
  width: 50%;
  margin: 0 auto;
  padding: 40px;
  background-color: rgba(10, 10, 10, 0.77);
  border: 2px ridge rgba(238, 238, 238, 0.13);
  border-radius: 5px;
  box-shadow: 0 -5px 10px 1px rgba(16, 16, 16, 0.57);
}

.login {
  width: 45%;
  float: left;
  text-align: left;
  padding-right: 40px;
}

h2 {
  font-size: 35px;
  text-align: left;
  color: #fff;
  font-weight: 100;
  margin-bottom: 20px;
}

input[type="text"],
input[type="password"] {
  width: 93.4%;
  margin-bottom: 20px;
  padding: 10px;
  float: left;
  background-color: transparent;
  border: none;
  font-size: 15px;
  border-bottom: 1px solid rgba(238, 238, 238, 0.41);
  outline: none;
  color: #fff;
  transition: all 0.1ms;
}

.send-button {
  margin-bottom: 20px;
}

.send-button input[type="button"] {
  width: 60%;
  padding: 10px 0;
  font-size: 16px;
  font-weight: 100;
  background-color: transparent;
  color: #ccc;
  border: 1px solid rgba(238, 238, 238, 0.41);
  border-width: thin;
  cursor: pointer;
  outline: none;
  transition: 0.5s all;
  text-decoration: none;
}

.send-button input[type="button"]:hover {
  background-color: #000;
  border: 1px solid #fff;
  color: #fff;
  transition: 0.5s all;
  text-decoration: none;
}

.login a {
  color: #ccc;
}

.registerr {
  height: 1000px;
  font-family: "Roboto", sans-serif;
  text-align: center;
  background: url("../assets/backgroundd.jpg");
  background-repeat: no-repeat;
  background-attachment: fixed;
  background-position: center;
  background-size: cover;
}

.register {
  width: 44%;
  float: left;
  border-left: 1px solid #ddd;
  padding-left: 40px;
  text-align: left;
}

.register p {
  color: #ccc;
  margin-bottom: 10px;
}

.register p a {
  color: #ccc;
}

.register p a:hover {
  color: #fff;
}

.register input[type="text"].on {
  border-bottom: 1px solid rgba(255, 0, 0, 0.747);
}

.register_from {
  margin-top: 100px;
}

.tick {
  list-style: none;
  display: inline-block;
  width: 100%;
  margin-bottom: 20px;
}

.tick li input[type="checkbox"] {
  display: none;
}

.tick li input[type="checkbox"] + label {
  position: relative;
  padding-left: 30px;
  border: #f0f8ff;
  display: inline-block;
  font-size: 15px;
  color: #eee;
}

.tick li input[type="checkbox"] + label span:first-child {
  width: 17px;
  height: 17px;
  display: inline-block;
  border: 1px solid #eee;
  position: absolute;
  top: -3px;
  left: 0;
  bottom: 4px;
}

.tick li input[type="checkbox"]:checked + label span:first-child:before {
  content: "";
  background: url(../assets/tick.png) no-repeat;
  position: absolute;
  left: 3px;
  top: 3px;
  font-size: 10px;
  width: 10px;
  height: 10px;
}
</style>