<template>
  <div id="app">
    <div class="cms_login_container">
      <div class="login_header">
        <div class="cms_login_text">欢迎登录</div>
      </div>
      <div class="cms_login_table">
        <form>
          <div class="divBox">
            <input type="text" placeholder="请输入账号" v-model="user.number" />
          </div>
          <div class="divBox">
            <input
              type="password"
              placeholder="请输入密码"
              v-model="user.password"
            />
          </div>
          <div class="divBox margin_top60">
            <button class="login_btn" type="button" @click="submit">
              登录
            </button>
          </div>
        </form>
      </div>
    </div>
    <alertdialog />
  </div>
</template>

<script>
import { login } from "./api/Login";
export default {
  components: {
    alertdialog: () => import("@/components/AlertDialog")
  },
  data: () => ({
    user: { number: null, password: null }
  }),
  methods: {
    submit() {
      login(this.user);
      this.$nextTick(() => {
        this.user = { number: null, password: null };
      });
    }
  }
};
</script>

<style>
.login_header {
  display: flex;
  height: 100px;
  width: 100%;
  justify-content: center;
  line-height: 80px;
}
.role {
  float: right;
  margin-top: 5px;
  margin-right: 5px;
  /* margin-left: auto; */
}
.role select {
  border: none;
}

.cms_login_container {
  width: 500px;
  height: 360px;
  border-radius: 10px;
  border: 1px solid #ccc;
  box-shadow: 0px 0px 10px #ccc;
  /* background-color: rgb(147, 248, 248); */
  background-color: #fff;
  margin: auto;
  opacity: 0.7;
}

.cms_login_text {
  /* height: 100px;
  width: 100%;
  line-height: 80px; */
  text-align: center;
  font-size: 30px;
}

.cms_login_table {
  font-size: 18px;
}

/* 统一盒子样式 */
.divBox {
  height: 50px;
  width: 100%;
  line-height: 50px;
  text-align: center;
}

input {
  height: 30px;
  width: 290px;
  padding-left: 5px;
  border-radius: 5px;
  outline: none;
}

input:focus {
  border-radius: 5px;
  outline: none;
  border: 2px solid #66afe9;
  box-shadow: inset 0 2px 2px rgba(0, 0, 0, 0.075),
    0 0 8px rgba(102, 175, 233, 0.6);
}

.margin_right10 {
  margin-right: 10px;
}

.margin_top60 {
  margin-top: 60px;
}

.login_btn {
  width: 360px;
  height: 100%;
  background-color: #1360a7;
  border-radius: 10px;
  outline: none;
  font-size: 24px;
  color: white;
  letter-spacing: 24px;
}

.login_btn:hover {
  background-color: #1e5d5d;
}
</style>
