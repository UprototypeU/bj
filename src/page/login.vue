<template>
  	<div class="login_page fillcontain aa">
	  	<transition name="form-fade" mode="in-out">
	  		<section class="form_contianer" v-show="showLogin">
		    	<el-form :model="loginForm" :rules="rules" ref="loginForm">
            <h3>贸易金融平台</h3>
					<el-form-item prop="username">
						<el-input v-model="loginForm.username" placeholder="用户名"></el-input>
					</el-form-item>
					<el-form-item prop="password">
						<el-input type="password" placeholder="密码" v-model="loginForm.password"></el-input>
					</el-form-item>
					<el-form-item class="btn-wp">
				    	<el-button type="primary" @click="submitForm('loginForm')" class="submit_btn">登陆</el-button>
				  	</el-form-item>
				</el-form>
				<p><router-link class="fl" to="/forgetPwdStep1">忘记密码</router-link><router-link class="fr" to="/loginFlow">注册账户</router-link></p>
	  		</section>
	  	</transition>
  	</div>
</template>

<script>
import { login, getAdminInfo } from "@/api/getData";
import { mapActions, mapState } from "vuex";
export default {
  data() {
    return {
      loginForm: {
        username: "",
        password: ""
      },
      rules: {
        username: [
          { required: true, message: "请输入用户名", trigger: "blur" }
        ],
        password: [{ required: true, message: "请输入密码", trigger: "blur" }]
      },
      showLogin: true
    };
  },
  mounted() {
    // this.showLogin = true;
    // if (!this.adminInfo.id) {
    // 	this.getAdminData()
    // }
  },
  computed: {
    // ...mapState(['adminInfo']),
  },
  methods: {
    // ...mapActions(['getAdminData']),
    async submitForm(formName) {
      
      if(this.loginForm.username != '' && this.loginForm.password != ''){
        this.$message({
          type: "success",
          message: "登录成功"
        });
        this.$router.push("myBanchBacklog");        
      }else{
        this.$message({
          showClose: true,
          message: '请先认证企业身份',
          type: 'warning'
        });
        this.$router.push("signFlowFirmApprove");
      }
      // this.$refs[formName].validate(async (valid) => {
      // 	if (valid) {
      // 		const res = await login({user_name: this.loginForm.username, password: this.loginForm.password})
      // 		if (res.status == 1) {
      // 			this.$message({
      //                 type: 'success',
      //                 message: '登录成功'
      //             });
      // 			this.$router.push('manage')
      // 		}else{
      // 			this.$message({
      //                 type: 'error',
      //                 message: res.message
      //             });
      // 		}
      // 	} else {
      // 		this.$notify.error({
      // 			title: '错误',
      // 			message: '请输入正确的用户名密码',
      // 			offset: 100
      // 		});
      // 		return false;
      // 	}
      // });
    }
  },
  watch: {
    // adminInfo: function (newValue){
    // 	console.log(newValue)
    // 	if (newValue.id) {
    // 		this.$message({
    //             type: 'success',
    //             message: '检测到您之前登录过，将自动登录'
    //         });
    // 		this.$router.push('manage')
    // 	}
    // }
  }
};
</script>

<style lang="less" scoped>
@import "../style/mixin";
.login_page {
  background: url(../assets/img/login-bj.png) center center no-repeat;
  height: 100%;
}
.manage_tip {
  position: absolute;
  width: 100%;
  top: -100px;
  left: 0;
  p {
    font-size: 34px;
    color: #fff;
  }
}
.form_contianer {
  .wh(840px, 440px);
  .ctp(840px, 440px);
  padding: 70px 60px 0 460px;
  text-align: center;
  background-color: #fff;
  box-sizing: border-box;
  background: url(../assets/img/login-box.png) left center no-repeat #fff;
  h3 {
    font-size: 22px;
    color: #4a6cd5;
    margin-bottom: 30px;
    text-align: left;
  }
  .btn-wp{
    margin-top: 40px;
  }
  .submit_btn {
    width: 100%;
    font-size: 16px;
  }
  a{
    color: #4A6CD5 ;
  }
}
.tip {
  font-size: 12px;
  color: red;
}
.form-fade-enter-active,
.form-fade-leave-active {
  transition: all 1s;
}
.form-fade-enter,
.form-fade-leave-active {
  transform: translate3d(0, -50px, 0);
  opacity: 0;
}
</style>
