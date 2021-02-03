<template>
  <div class="login_container">
    <div class="login_box">
      <!--头像区域-->
      <div class="avatar_box">
        <img src="../assets/logo.png">
      </div>
      <!--登录表单区域-->
      <el-form ref="loginFormRef" :model="loginForm" :rules="loginFormRules" class="login_form">
        <!--用户名-->
        <el-form-item prop="username">
          <el-input v-model="loginForm.username" prefix-icon="el-icon-user" placeholder="请输入登录名称"></el-input>
        </el-form-item>
        <!--密码-->
        <el-form-item prop="password">
          <el-input v-model="loginForm.password" prefix-icon="el-icon-view" placeholder="请输入密码" type="password"></el-input>
        </el-form-item>
        <!--按钮区域-->
        <el-form-item class="btns">
          <el-button @click="login" type="primary">登录</el-button>
          <el-button @click="resetForm('loginFormRef')" type="info" plain>重置</el-button>
        </el-form-item>
      </el-form>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      // 这是登录表单的数据绑定对象
      loginForm: {
        username: 'admin',
        password: '123456'
      },
      // 这是表单的验证规则
      loginFormRules: {
        username: [
          { required: true, message: '请输入登录名称', trigger: 'blur' },
          { min: 2, max: 10, message: '长度在 2 到 10 个字符', trigger: 'blur' }
        ],
        password: [
          { required: true, message: '请输入密码', trigger: 'blur' },
          { min: 6, max: 10, message: '长度在 6 到 10 个字符', trigger: 'blur' }
        ]
      }
    }
  },
  methods: {
    // 重置表单按钮
    resetForm () {
      this.$refs.loginFormRef.resetFields()
    },
    login () {
      this.$refs.loginFormRef.validate((valid) => {
        if (valid) {
          // this.$message.success('登录成功')
          this.$message({
            message: '登录成功',
            type: 'success',
            center: true
          })
          window.sessionStorage.setItem('token', Date.now())
          this.$router.push('/home')
        } else {
          this.$message.error('登录失败！')
          return false
        }
      })
    }
  }
}
</script>

<style lang="less" scoped>
  .login_container{
    background-color: #2b4b6b;
    height: 100%;
  }
  .login_box{
    width: 450px;
    height: 300px;
    background-color: white;
    border-radius: 3px;
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%,-50%);

    .avatar_box{
      height: 130px;
      width: 130px;
      border: 1px solid #ffffff;
      border-radius: 50%;
      padding: 10px;
      box-shadow: 0 0 10px #dddddd;
      position: absolute;
      left: 50%;
      transform: translate(-50%,-50%);
      background-color: white;
      img{
        height: 100%;
        width: 100%;
        border-radius: 50%;
        background-color: #eeeeee;
      }
    }
  }

  .login_form{
    position: absolute;
    bottom: 0;
    width: 100%;
    padding: 0 20px;
    box-sizing: border-box;
  }
  .btns{
    display: flex;
    justify-content: flex-end;
  }
</style>
