<template>
    <div class="all">
        <div class="head">
            <div class="header">系统登陆</div>
            <div class="icon">v</div>
        </div>
        <input placeholder="账号" class="num">
        <input placeholder="密码" class="num">
       <div class="yzm">
            <input placeholder="验证码 单击图片刷新" class="yzmnum">
            <img src="./image/yzm.jpg" class="yzmimg">
       </div>
        <div class="bottom">
            <div class="cz">重置</div>
            <div class="dl">登陆</div>
        </div>
        <div id="app">
            <input v-model="date">
			{{date}}
		</div>
    </div>
  
</template>

<script>
export default {
    name:'login',
    
   data() {
       return {
           date:new Date(new Date()-0 + 6*24*60*60*1000)
       }
   },
   methods: {
       
   },

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
    .yzm
        width 300px
        height 40px
        margin 10px 45px
        .yzmnum
            height 40px
            line-height 40px
            width 150px
            float left
        .yzmimg
            height 40px
            line-height 40px
            width 100px
            float right 
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
</style>