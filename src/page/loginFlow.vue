<template>
    <div class="fillcontain register">
        <div class="table_container">
            <h3>用户注册</h3>
            <el-form :model="ruleForm" :rules="rules" ref="ruleForm" class="demo-ruleForm">
                <el-form-item prop="uesr">
                    <el-input type="text" placeholder="请输入用户名" v-model="ruleForm.user" auto-complete="off"></el-input>
                </el-form-item>
                <el-form-item prop="pass">
                    <el-input type="password" placeholder="请输入密码" v-model="ruleForm.pass" auto-complete="off"></el-input>
                </el-form-item>
                <el-form-item prop="checkPass">
                    <el-input type="password" placeholder="请再次输入密码" v-model="ruleForm.checkPass" auto-complete="off"></el-input>
                </el-form-item>
                <el-form-item prop="elm">
                    <el-input type="password" placeholder="请输入您的邮箱" v-model="ruleForm.elm" auto-complete="off"></el-input>
                </el-form-item>
                <el-form-item>
                  <loginSider></loginSider>
                </el-form-item>
                <el-form-item prop="type">
                    <el-checkbox v-model="ruleForm.checked" label="我已认真阅读并同意"></el-checkbox><a href="#">《用户注册协议》</a>
                </el-form-item>
                <el-form-item>
                    <el-button type="primary" @click="submitForm('ruleForm')" style="width:100%;">注册</el-button>
                </el-form-item>
            </el-form>
            <p class="to-login">已有账号？ <router-link to="/">点此登录</router-link></p>
        </div>
    </div>
</template>

<script>
import loginSider from "../components/loginSider";
export default {
  data() {
    var validatePass = (rule, value, callback) => {
      if (value === "") {
        callback(new Error("请输入密码"));
      } else {
        if (this.ruleForm.checkPass !== "") {
          this.$refs.ruleForm.validateField("checkPass");
        }
        callback();
      }
    };
    var validatePass1 = (rule, value, callback) => {
      if (this.ruleForm.user) {
        callback();
      } else {
        callback(new Error("请输入正确的用户名"));
      }
    };
    var validatePass2 = (rule, value, callback) => {
      if (value === "") {
        callback(new Error("请再次输入密码"));
      } else if (value !== this.ruleForm.pass) {
        callback(new Error("两次输入密码不一致!"));
      } else {
        callback();
      }
    };
    var validatePass3 = (rule, value, callback) => {
      if (this.ruleForm.checked) {
        callback();
      } else {
        callback(new Error("必须勾选!"));
      }
    };
    return {
      value1: "",
      ruleForm: {
        pass: "",
        checkPass: "",
        user: "",
        checked: "",
        elm:''
      },
      rules: {
        pass: [{ validator: validatePass, trigger: "blur" }],
        uesr: [{ validator: validatePass1, trigger: "blur" }],
        checkPass: [{ validator: validatePass2, trigger: "blur" }],
        type: [{ validator: validatePass3, trigger: "change" }]
      }
    };
  },
  components: {
    loginSider
  },
  created() {},
  methods: {
    submitForm(formName) {
      this.$refs[formName].validate(valid => {
        if (valid) {
          // alert("submit!");
          this.$router.push("regSuc");
        } else {
          console.log("error submit!!");
          return false;
        }
      });
    },
    resetForm() {
      this.$router.push("/");
    }
  }
};
</script>

<style lang="less" scoped>
@import "../style/mixin";
.register {
  background: url(../assets/img/login-bj.png) center center no-repeat;
}
.table_container {
  .wh(750px,700px);
  .ctp(750px,700px);
  background: #fff;
  box-sizing: border-box;
  padding: 70px 220px 0;
  h3{
     font-size: 22px;
      color: #4a6cd5;
      margin-bottom: 30px;
      text-align: center;
  }
  a{
    color: #4a6cd5;
  }
  .to-login{
    margin-top: 50px;
    padding-top: 30px;
    text-align: center;
    border-top: 1px solid #e1e1e1;
  }
}
</style>


