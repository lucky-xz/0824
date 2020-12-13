<template>
  <div class="login">
    <div class="con">
      <h2>登录</h2>
      <input
        type="text"
        placeholder="请输入账号"
        v-model="user.username"
      /><br />
      <input
        type="text"
        placeholder="请输入密码"
        v-model="user.password"
      /><br />
      <div class="btn"><button @click="login">登录</button></div>
    </div>
  </div>
</template>

<script>
import { requserLogin } from "../../util/request";
import {mapActions,mapGetters} from 'vuex'
export default {
  components: {},
  data() {
    return {
      user: {
        username: "",
        password: "",
      },
    };
  },
  methods: {
    ...mapActions({
     requestuserList:'user/requestuserList'
    }),
    login() {
      requserLogin(this.user).then((res) => {
        if (res.data.code == 200) {
          // console.log(res.data.list);
          this.requestuserList(res.data.list);
          this.$router.push("/index/home");
        } else {
          alert(res.data.msg);
        }
      });
    },
  },
  mounted() {},
  computed: {},
  watch: {},
};
</script>
<style>
.login {
  width: 100vw;
  height: 100vh;
  background: linear-gradient(to right, #563443, #303d60);
  overflow: hidden;
  text-align: center;
}
.con {
  width: 300px;
  height: 200px;
  background-color: #fff;
  margin: 100px auto;
  border-radius: 10px;
  padding: 20px;
}
.con input {
  width: 60%;
  height: 25px;
  margin-top: 10px;
  outline: none;
}
.con .btn {
  width: 62%;
  height: 30px;
  margin: 20px auto;
  /* background-color: red; */
}
.con .btn button {
  width: 100%;
  height: 30px;
  background-color: #409eff;
  color: #fff;
  outline: none;
  border: none;
}
</style>