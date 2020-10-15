<template>
  <Form ref="loginFormNew" :model="form" :rules="rules" @keydown.enter.native="handleSubmit">
    <div v-if="qcodeForm === false">
        <FormItem prop="phone">
            <p>手机号码</p>
            <Input v-model="form.phone" placeholder="请输入手机号码"></Input>
        </FormItem>
        <FormItem prop="qrcode">
            <p>验证码</p>
            <Input v-model="form.qrcode" placeholder="请输入验证码">
                <span slot="append" :disabled="qrcodeDisabled" @click="getVerifyCode">{{verifyText}}</span>
            </Input>
        </FormItem>
    </div>
    <div class="qcorde_box" v-else>
        <h3 class="txc">扫码登录</h3>
        <p  class="txc">请使用微信扫码登录</p>
        <img class="qr_code" :src="qrUrl" />
    </div>
    <div>
       <Button @click="handleSubmit" type="primary" long>登录</Button> 
       <a href="javavascript:;" class="bt_lnk" @click="showQcodeForm">{{qFormTxt}}</a> 
    </div>
  </Form>
</template>
<script>
export default {
  name: 'LoginFormNew',
  data () {
    var validateMobilePhone = (rule, value, callback) => {
      if (value === '') {
        callback(new Error('手机号不能为空!'));
      } else {
        var reg = /^1[3456789]\d{9}$/;
        if(!reg.test(value)){
        callback(new Error('请输入有效的手机号码!'));
        return;
        }
        callback();
      }
    };

    var validateQrcode = (rule, value, callback) => {
      if (value === '') {
        callback(new Error('验证码不能为空'));
      }else{
        var reg = /^\d{6}$/;
        if(!reg.test(value)){
          callback(new Error('请输入正确的验证码'));
          return;
        }
        callback();
      } 
    };
    return {
      form: {
        phone: '',
        qrcode: ''
      },
      rules: {
         phone: [
            //{ required: true, validator: validateMobilePhone, trigger: 'blur' }
         ], 
         qrcode: [
           //{ required: true, validator: validateQrcode, trigger: 'blur' }
         ]
      },
      qcodeForm: false,
      qrcodeDisabled: false,
      verifyText: '',
      qFormTxt: '二维码登录',
      qrUrl: require('../../static/img/qcode.png')
    }
  },
  mounted () {
    this.verifyText = '点击获取'
  },
  methods: {
    // 切换验证码/二维码登录
    showQcodeForm () {
      this.qFormTxt = this.qcodeForm === false ? '手机号登录' : '二维码登录'
      this.qcodeForm = !this.qcodeForm
    },
    // 获取验证码
    getVerifyCode () {
      this.validateBtn()
    },
    // 验证码倒计时
    validateBtn () {
      // 倒计时
      let time = 60
      let timer = setInterval(() => {
        if (time === 0) {
          clearInterval(timer)
          this.qrcodeDisabled = false
          this.verifyText = '点击获取'
        } else {
          this.verifyText = time + '秒后重试'
          this.qrcodeDisabled = true
          time--
        }
      }, 1000)
    },
    // 提交
    handleSubmit () {
      this.$refs.loginFormNew.validate((valid) => {
        if (valid) {
          this.$emit('on-success-valid', {
            phone: this.form.phone,
            qrcode: this.form.qrcode
          })
          this.$refs.['loginFormNew'].resetFields();
        }
      })
    }
  }
}
</script>
<style scoped>
.txc{
    text-align: center;
}
.bt_lnk{
    display:block;
    text-align: center;
    margin: 10px 0;
}
.qcorde_box{
    margin-bottom: 10px;
}
.qr_code{
    display: flex;
    justify-content: center;
    align-items: center;
    width:200px;
    height: 200px;
    margin: 0 auto;
    overflow: hidden;
}
</style>
