<template>
  <div id="login">
    <h4>用户名</h4>
    <el-input v-model="username" placeholder="用户名"></el-input>
    <h4>密码</h4>
    <el-input v-model="password" type="password" placeholder="密码" @keyup.enter.native="onLogin"></el-input>
    <el-button type="primary" size="medium" @click="onLogin">立即登录</el-button>
    <p class="notice">没有账号？
      <router-link to="/register">注册新用户</router-link>
    </p>
  </div>
</template>

<script lang="ts">
import {mapActions} from 'vuex';

export default {
  name: 'Login',
  data() {
    return {
      username: 'hahaha',
      password: '123456'
    };
  },
  methods: {
    ...mapActions([
        'login'
    ]),
    onLogin() {
      this.login({username: this.username, password: this.password})
          .then(() => {
            this.$router.push({path: this.$route.query.redirect || '/'});
          });
    }
  }
};
</script>

<style lang="scss" scoped>
#login, #register {
  display: grid;
  justify-content: center;
  padding-top: 30px;

  h4 {
    margin: 10px 0 5px;
  }

  p {
    margin: 5px 0;
  }

  input {
    width: 400px;
  }

  .error {
    font-size: 12px;
    color: #f00;
  }

  button {
    margin-top: 10px;
    justify-self: start;
  }

  .notice {
    font-size: 12px;
    text-align: center;
    margin-top: 30px;

    a {
      color: #42b983;
    }
  }
}
</style>
