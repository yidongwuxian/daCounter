<style lang="less">
  @import './login.less';
</style>

<template>
  <div class="login">
    <div class="login_header">
        <a class="logo" href="javascript:;">logo</a>
    </div>
    <div class="login_bd">
        <Card>
          <div class="login_con">
                <div class="form_bd_img">
                   <img :src="f_bd_img" />
                </div>
                <div class="form_cn">
                    <login-form-new  @on-success-valid="handleSubmit"></login-form-new>
                </div>
            </div>
        </Card>
    </div>
  </div>
</template>

<script>
import LoginFormNew from '_c/login_form_new'
import { mapActions } from 'vuex'
export default {
  data () {
    return {
      f_bd_img: require('../../static/img/login_bd_img1.png')
    }
  },
  components: {
    LoginFormNew
  },
  methods: {
    ...mapActions([
      'handleLogin',
      'getUserInfo'
    ]),
    handleSubmit ({ phone, qrcode }) {
      this.handleLogin({ phone, qrcode }).then(res => {
        this.getUserInfo().then(res => {
          this.$router.push({
            name: this.$config.homeName
          })
        })
      })
    }
  }
}
</script>

<style>
.f_bd_img{
  display: block;
  width: 367px;
  height: 245px;
}
</style>
