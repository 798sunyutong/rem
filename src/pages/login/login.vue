<template>
    <div class="all">
        <div class="head">
            <div class="header">系统登陆</div>
            <div class="icon">v</div>
        </div>
        <input placeholder="账号" class="num" v-model="account" @blur="accountblur()">
        <input placeholder="密码" class="num" v-model="password" @blur="passwordblur()">
        <input placeholder="验证码 单击图片刷新" class="yzmnum" v-model="authcode" @blur="authcodeblur()">
        <div class="code" @click="refreshCode()">
            <SIdentify :identifyCode="identifyCode"></SIdentify>
        </div>
        <div class="bottom">
            <div class="cz" @click="ferstclear()">重置</div>
            <div class="dl">登陆</div>
        </div>
        <!-- <div id="app"  @click="fff()">
            <input v-model="date">
			{{date}}
		</div> -->
    </div>
  
</template>

<script>
import SIdentify from './identify'
export default {
    name:'login',
    components:{SIdentify:SIdentify},
    data() {
        return {
            //    date:new Date(new Date()-0 + 6*24*60*60*1000)，获取当前日期的6天后
            identifyCodes: "1234567890",
            identifyCode: "",
            account:'',
            password:'',
            authcode:'',
        }
        
    },
    mounted() {
            this.identifyCode = "";
            this.makeCode(this.identifyCodes, 4);//四位数的验证码
        },  
    methods: {
    //   fff(){
    //     console.log("%cparams","color:yellow",this.date)带颜色的console.log()
    //   } 
        //生成一个随机数，用在验证码四位数的随机生成
        randomNum(min, max) {
      return Math.floor(Math.random() * (max - min) + min);
    },
    //点击图片刷新验证码
    refreshCode() {
      this.identifyCode = "";
      this.makeCode(this.identifyCodes, 4);//与makeCode(o, l)一一对应o=this.identifyCodes,l=4
    },
    //用来生成四位随机数
     makeCode(o, l) {//o指this.identifyCodes，l不是数字1 ，是L。
      for (let i = 0; i < l; i++) {//l不是数字1 ，是L。L参数的值为数字4
        this.identifyCode += this.identifyCodes[//+=生成四个数
          this.randomNum(0, this.identifyCodes.length)
        ];
      }
      console.log(this.identifyCode);
    },
    //重置按钮清空
    ferstclear(){
        this.authcode = ''
        this.password=''
        this.account=''
    },
    //账号校验
    accountblur(){
        //帐号是否合法(字母开头，允许5-16字节，允许字母数字下划线)：
        var reg=/^[a-zA-Z][a-zA-Z0-9_]{4,15}$/
        var _that = this
        if(this.account ==''|| this.account == undefined ){
            this.$toast("账号格式为字母开头，5-16个字符，允许字母数字下划线")
        }else if(!reg.test(this.account)){
            this.$toast("账号格式为字母开头，5-16个字符，允许字母数字下划线")
        }
    },
    //手机号校验
    passwordblur(){
        //密码包含 数字,英文,字符中的两种以上，长度6-20
        var reg=/^$^(?![0-9]+$)(?![a-z]+$)(?![A-Z]+$)(?!([^(0-9a-zA-Z)])+$).{6,20}$/
        var _this=this
        if(this.password=="" || this.password==undefined){
            this.$toast('密码包含 数字,英文,字符中的两种以上，长度6-20')
        }else if(!reg.test(this.password)){
            this.$toast('密码包含 数字,英文,字符中的两种以上，长度6-20')
        }
    },
    //验证码是否正确
    authcodeblur(){
        console.log("%cparams","color:red", this.authcode)
        if(this.authcode!=this.identifyCode || this.authcode=='' || this.authcode==undefined){
            this.authcode=''
            this.$toast('请正确输入的验证码')
        }
    },
    
  }
}
</script>

<style lang="stylus" scoped>
.all
    height 400px
    width 400px
    background-color #ccc
    .head
        width 400px
        height 90px
        line-height 90px
        .header
            font-size 30px
            width 230px
            display inline-block
            text-align center
        .icon
            width 40px
            font-size 30px
            height 40px
            line-height 40px            
            background-color #1A6BE6
            display inline-block
            text-align center
    .num
        width 300px
        height 40px
        margin 10px
    .bottom
        width 300px
        height 40px
        margin 20px 45px
        .cz
            width 140px
            height 40px
            line-height 40px
            text-align center
            border 1px black solid
            display inline-block
            background-color #1A6BE6
            border-radius 4px
            margin-right 10px
        .dl
            width 140px
            height 40px
            line-height 40px
            text-align center
            border 1px black solid
            display inline-block
            background-color #1A6BE6
            border-radius 4px
    .yzmnum
        height 40px
        line-height 40px
        width 150px 
        float left
        margin 20px 25px 20px 45px
        // margin: 400px auto;
        // width: 114px;
        // height: 40px;
        border 1px solid red;
    .code
        margin 20px 0px
        width 114px
        height 40px
        margin-right 45px
        border 1px solid red
        display inline-block
</style>