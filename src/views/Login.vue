<template>
  <div class="login_container">
    <div class="login_box">
        <el-form  label-width="80px" class="login_form" :model="loginForm">
            <!--用户名-->
            <el-form-item label="userName">
                <el-input v-model="loginForm.username"></el-input>
            </el-form-item>
            <!--密码-->
            <el-form-item label="password">
                <el-input v-model="loginForm.password" type="password"></el-input>
            </el-form-item>
            <!--按钮-->
            <el-form-item class="btn">
                <el-button type="primary" @click="login()">登录</el-button>
                 <el-button type="info">重置</el-button>
            </el-form-item>
        </el-form>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      loginForm: {
        username: '',
        password: ''
      }
    }
  },
  methods: {
    async login () {
      var { data: res } = await this.$http.post('login', this.loginForm)
      if (res.meta.status !== 200) {
        return console.log('failure')
      } else {
        console.log('sucess')
        window.sessionStorage.setItem('token', res.data.token)
        this.$router.push('/home')
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.login_container{
    background-color: blue;
    height: 100%;
    width: 100%;
    .login_box{
        width:450px;
        height: 300px;
        position: absolute;
        left: 50%;
        top:50%;
        border: 1px solid black;
        background: white;
        transform: translate(-50%,-50%);
        .login_form{
            position: absolute;
            bottom:0;
            width: 100%;
            padding: 0 10px;
            box-sizing: border-box;
            .btn{
                display: flex;
                justify-content: flex-end;
            }
        }
    }
}
</style>
