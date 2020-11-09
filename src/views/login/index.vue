<template>
  <div class="login-container bg">
    <!--    <el-form ref="loginForm" :model="loginForm" :rules="loginRules" class="login-form" auto-complete="on" label-position="left">-->
    <!--      <div class="title-container">-->
    <!--        <h3 class="title">-->
    <!--          {{ $t('login.title') }}-->
    <!--        </h3>-->
    <!--        <lang-select class="set-language" />-->
    <!--      </div>-->

    <!--      <el-form-item prop="username">-->
    <!--        <span class="svg-container">-->
    <!--          <svg-icon icon-class="user" />-->
    <!--        </span>-->
    <!--        <el-input-->
    <!--          ref="username"-->
    <!--          v-model="loginForm.username"-->
    <!--          :placeholder="$t('login.username')"-->
    <!--          name="username"-->
    <!--          type="text"-->
    <!--          auto-complete="on"-->
    <!--        />-->
    <!--      </el-form-item>-->

    <!--      <el-form-item prop="password">-->
    <!--        <span class="svg-container">-->
    <!--          <svg-icon icon-class="password" />-->
    <!--        </span>-->
    <!--        <el-input-->
    <!--          ref="password"-->
    <!--          v-model="loginForm.password"-->
    <!--          :type="passwordType"-->
    <!--          :placeholder="$t('login.password')"-->
    <!--          name="password"-->
    <!--          auto-complete="on"-->
    <!--          @keyup.enter.native="handleLogin"-->
    <!--        />-->
    <!--        <span class="show-pwd" @click="showPwd">-->
    <!--          <svg-icon :icon-class="passwordType === 'password' ? 'eye' : 'eye-open'" />-->
    <!--        </span>-->
    <!--      </el-form-item>-->

    <!--      <el-button :loading="loading" type="primary" style="width:100%;margin-bottom:30px;" @click.native.prevent="handleLogin">-->
    <!--        {{ $t('login.logIn') }}-->
    <!--      </el-button>-->

    <!--      <div style="position:relative">-->
    <!--        <div class="tips">-->
    <!--          <span>{{ $t('login.username') }} : admin</span>-->
    <!--          <span>{{ $t('login.password') }} : {{ $t('login.any') }}</span>-->
    <!--        </div>-->
    <!--        <div class="tips">-->
    <!--          <span style="margin-right:18px;">-->
    <!--            {{ $t('login.username') }} : editor-->
    <!--          </span>-->
    <!--          <span>{{ $t('login.password') }} : {{ $t('login.any') }}</span>-->
    <!--        </div>-->

    <!--        <el-button class="thirdparty-button" type="primary" @click="showDialog=true">-->
    <!--          {{ $t('login.thirdparty') }}-->
    <!--        </el-button>-->
    <!--      </div>-->
    <!--    </el-form>-->

    <!--    <el-dialog :title="$t('login.thirdparty')" :visible.sync="showDialog">-->
    <!--      {{ $t('login.thirdpartyTips') }}-->
    <!--      <br>-->
    <!--      <br>-->
    <!--      <br>-->
    <!--      <social-sign />-->
    <!--    </el-dialog>-->
    <div class="schoollogo">
      <div class="school_container">
        <div class="school">
          <img src="../../assets/bg/logo.png">
        </div>
        <div class="school_title">
          <span>石家庄人民医专人事管理系统</span>
        </div>
      </div>
    </div>
    <div class="login_container">
      <div class="picture_container">
        <img src="../../assets/bg/tea_pic.png">
      </div>
      <div class="login_card login-container">
        <el-form ref="loginForm" :model="loginForm" :rules="loginRules" class="login-form" auto-complete="on" label-position="left">
          <div class="title-container">
            <h4 class="title">
              {{ $t('login.title') }}
            </h4>
            <lang-select class="set-language" />
          </div>

          <el-form-item prop="username">
            <span class="svg-container">
              <svg-icon icon-class="user" />
            </span>
            <el-input
              ref="username"
              v-model="loginForm.username"
              :placeholder="$t('login.username')"
              name="username"
              type="text"
              auto-complete="on"
            />
          </el-form-item>
          <el-form-item prop="password">
            <span class="svg-container">
              <svg-icon icon-class="password" />
            </span>
            <el-input
              ref="password"
              v-model="loginForm.password"
              :type="passwordType"
              :placeholder="$t('login.password')"
              name="password"
              auto-complete="on"
              @keyup.enter.native="handleLogin"
            />
            <span class="show-pwd" @click="showPwd">
              <svg-icon :icon-class="passwordType === 'password' ? 'eye' : 'eye-open'" />
            </span>
          </el-form-item>

          <el-button :loading="loading" type="primary" style="width:100%;margin-bottom:30px;" @click.native.prevent="handleLogin">
            {{ $t('login.logIn') }}
          </el-button>

          <div style="position:relative">
            <div class="tips">
              <span />
              <span />
            </div>
            <div class="tips">
              <span style="margin-right:18px;" />
              <span />
            </div>

            <el-button class="thirdparty-button" type="primary">
              <!--              {{ $t('login.thirdparty') }}-->
              忘记密码
            </el-button>
          </div>
        </el-form>
      </div>
    </div>
    <div class="copyrightContainer">
      <span style="font-size: 12px">Copyright&nbsp;&nbsp;&nbsp;中科智禾教育大数据中心   ©2020</span>
    </div>
  </div>
</template>

<script>
import { validUsername } from '@/utils/validate'
// import LangSelect from '@/components/LangSelect'
// import SocialSign from './socialsignin'

export default {
  name: 'Login',
  // components: { LangSelect, SocialSign },
  data() {
    const validateUsername = (rule, value, callback) => {
      if (!validUsername(value)) {
        callback(new Error('Please enter the correct user name'))
      } else {
        callback()
      }
    }
    const validatePassword = (rule, value, callback) => {
      if (value.length < 6) {
        callback(new Error('The password can not be less than 6 digits'))
      } else {
        callback()
      }
    }
    return {
      loginForm: {
        username: 'admin',
        password: '111111'
      },
      loginRules: {
        username: [{ required: true, trigger: 'blur', validator: validateUsername }],
        password: [{ required: true, trigger: 'blur', validator: validatePassword }]
      },
      passwordType: 'password',
      loading: false,
      showDialog: false,
      redirect: undefined
    }
  },
  watch: {
    $route: {
      handler: function(route) {
        this.redirect = route.query && route.query.redirect
      },
      immediate: true
    }
  },
  created() {
    // window.addEventListener('hashchange', this.afterQRScan)
  },
  mounted() {
    if (this.loginForm.username === '') {
      this.$refs.username.focus()
    } else if (this.loginForm.password === '') {
      this.$refs.password.focus()
    }
  },
  destroyed() {
    // window.removeEventListener('hashchange', this.afterQRScan)
  },
  methods: {
    showPwd() {
      if (this.passwordType === 'password') {
        this.passwordType = ''
      } else {
        this.passwordType = 'password'
      }
      this.$nextTick(() => {
        this.$refs.password.focus()
      })
    },
    handleLogin() {
      this.$refs.loginForm.validate(valid => {
        if (valid) {
          this.loading = true
          this.$store.dispatch('LoginByUsername', this.loginForm).then(() => {
            this.loading = false
            this.$router.push({ path: this.redirect || '/' })
          }).catch(() => {
            this.loading = false
          })
        } else {
          console.log('error submit!!')
          return false
        }
      })
    },
    afterQRScan() {
      // const hash = window.location.hash.slice(1)
      // const hashObj = getQueryObject(hash)
      // const originUrl = window.location.origin
      // history.replaceState({}, '', originUrl)
      // const codeMap = {
      //   wechat: 'code',
      //   tencent: 'code'
      // }
      // const codeName = hashObj[codeMap[this.auth_type]]
      // if (!codeName) {
      //   alert('第三方登录失败')
      // } else {
      //   this.$store.dispatch('LoginByThirdparty', codeName).then(() => {
      //     this.$router.push({ path: '/' })
      //   })
      // }
    }
  }
}
</script>

<style rel="stylesheet/scss" lang="scss">
  /* 修复input 背景不协调 和光标变色 */
  /* Detail see https://github.com/PanJiaChen/vue-element-admin/pull/927 */

  $bg: #e5e5e5;
  $light_gray: #1b3413;
  $cursor: #fff;

  @supports (-webkit-mask: none) and (not (cater-color: $cursor)) {
    .login-container .el-input input{
      color: $cursor;
      &::first-line {
        color: $light_gray;
      }
    }
  }

  /* reset element-ui css */
  .login-container {
    .el-input {
      display: inline-block;
      height: 47px;
      width: 85%;
      input {
        background: transparent;
        border: 0px;
        -webkit-appearance: none;
        border-radius: 0px;
        padding: 12px 5px 12px 15px;
        color: $light_gray;
        height: 47px;
        caret-color: $cursor;
        &:-webkit-autofill {
          box-shadow: 0 0 0px 1000px $bg inset !important;
          -webkit-text-fill-color: $cursor !important;
        }
      }
    }
    .el-form-item {
      border: 1px solid rgba(255, 255, 255, 0.1);
      background: rgba(0, 0, 0, 0.1);
      border-radius: 5px;
      color: #454545;
    }
  }
</style>

<style rel="stylesheet/scss" lang="scss" scoped>
$bg:#2d3a4b;
$dark_gray:#889aa4;
$light_gray: #727272;
$bg:#283443;
$light_gray: #b4b4b4;
$cursor: #141519;

.login-container {
  min-height: 100%;
  width: 100%;
  overflow: hidden;
  .login-form {
    position: relative;
    width: 520px;
    max-width: 100%;
    padding: 50px 35px 0;
    margin: 0 auto;
    overflow: hidden;
  }
  .el-input {
    display: inline-block;
    height: 47px;
    width: 85%;
    input {
      background: transparent;
      border: 0px;
      -webkit-appearance: none;
      border-radius: 0px;
      padding: 12px 5px 12px 15px;
      color: $light_gray;
      height: 47px;
      caret-color: $cursor;
    }
  }
  .el-form-item {
    border: 1px solid rgba(255, 255, 255, 0.1);
    background: rgba(0, 0, 0, 0.1);
    border-radius: 5px;
    color: #454545;
  }
  .tips {
    font-size: 14px;
    color: #fff;
    margin-bottom: 10px;
    span {
      &:first-of-type {
        margin-right: 16px;
      }
    }
  }
  .svg-container {
    padding: 6px 5px 6px 15px;
    color: $dark_gray;
    vertical-align: middle;
    width: 30px;
    display: inline-block;
  }
  .title-container {
    position: relative;
    .title {
      font-size: 20px;
      color: $light_gray;
      margin: 0px auto 20px auto;
      text-align: center;
      font-weight: bold;
    }
    .set-language {
      color: #fff;
      position: absolute;
      top: 3px;
      font-size:18px;
      right: 0px;
      cursor: pointer;
    }
  }
  .show-pwd {
    position: absolute;
    right: 10px;
    top: 7px;
    font-size: 16px;
    color: $dark_gray;
    cursor: pointer;
    user-select: none;
  }
  .thirdparty-button {
    position: absolute;
    right: 0;
    bottom: 6px;
  }
}
  .bg{
    width: 100%;
    height:100%;
    min-width: 1200px;
    background: url("../../assets/bg/background.png")no-repeat;
    background-size: cover;
    background-position: center 0;
  }
  .schoollogo {
    width: 100%;
    height: 115px;
    text-align: center;
    position: relative;
    margin-top: 60px;
    display: flex;
  }
  .school_container{
    position: absolute;
    width: 1000px;
    left: 50%;
    transform: translate(-50%,0);
  }
  .school{
    float: left;
  }
  .school_title{
    margin-left: 20px;
    float: left;
    line-height: 115px;
    font-size: 50px;
    font-weight: bolder;
    color: white;
    letter-spacing: 8px;
  }
  .picture_container img {
    width: 350px;
    height: 350px;
  }
  .login_container{
    margin-top: 40px;
    display: flex;
    justify-content: center;
  }
  .picture_container {
    margin-right: 40px;
  }
  .login_card {
    margin-left: 120px;
    width: 350px;
    height: 350px;
    background-color: white;
    flex-direction: row;
    border-radius: 10px;
  }
.copyrightContainer{
  padding-top: 80px;
  text-align: center;
  margin-bottom: 20px;
  color: white;
}
</style>
