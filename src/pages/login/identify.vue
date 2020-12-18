<template>
    <div class="s-canvas">
        <canvas id="yzm" :width="contentWidth" :height="contentHeight"></canvas>
    </div>     
</template>

<script>

export default {
    name: 'SIdentify',
    data() {
        return {
        }
    },
    props:{
        //默认注册码
        identifyCode: {
            type: String,
            default: '1234'
        },
         // 字体最小值
        fontSizeMin: {
            type: Number,
            default: 16
        },       
         // 字体最大值
        fontSizeMax:{
            type:Number,
            default:40
        },
         // 验证码图片背景色最小值
        backgroundColorMin: {
            type: Number,
            default: 180
        },
        // 验证码图片背景色最大值
        backgroundColorMax: {
            type: Number,
            default: 240
        },
        //字体颜色最小值
        colorMin: {
            type: Number,
            default: 50
        },
        //字体颜色最大值
        colorMax: {
            type: Number,
            default: 160
        },
        //干扰线颜色最小值
        lineColorMin: {
            type: Number,
            default: 40
        },
        //干扰线颜色最大值
        lineColorMax: {
            type: Number,
            default: 180
        },
        // 背景干扰点最小值
        dotColorMin: {
            type: Number,
            default: 0
        },
        // 背景干扰点最大值
        dotColorMax: {
            type: Number,
            default: 255
        },
         //容器宽度
        contentWidth: {
            type: Number,
            default: 100
        },
        //容器高度
        contentHeight: {
            type: Number,
            default: 38
        }

    },
    methods: {
        
        //生成一个随机数
        randomNum (min, max) {
            return Math.floor(Math.random() * (max - min) + min)
        },
        //生成随机颜色
        randomColor (min, max) {
            let r = this.randomNum(min, max)
            let g = this.randomNum(min, max)
            let b = this.randomNum(min, max)
            return 'rgb(' + r + ',' + g + ',' + b + ')'
        },
        //生成的图形
        drawPic () {
            // debugger
            //获取当前画布
            let canvas = document.getElementById('yzm')
            //画布上绘图的环境
            let ctx=canvas.getContext('2d')
            //画布的文本基线，即绘制文本时的当前文本基线
            ctx.textBaseline = 'bottom'
            //绘制背景
            ctx.fillStyle = this.randomColor(this.backgroundColorMin, this.backgroundColorMax)
            ctx.fillRect(0, 0, this.contentWidth, this.contentHeight)
            console.log("%cparams","color:blue",ctx.fillRect)
             // 绘制文字
            for (let i = 0; i < this.identifyCode.length; i++) {
                this.drawText(ctx, this.identifyCode[i], i)
            //  Canvas 的文字绘制方法有：drawText()和 drawTextOnPath()。drawText()比较简单
            }
            this.drawLine(ctx)//画的线
            this.drawDot(ctx)
        },
        //生成随机文字
        drawText(ctx,txt,i){
            ctx.fillStyle = this.randomColor(this.colorMin, this.colorMax)
            ctx.font = this.randomNum(this.fontSizeMin, this.fontSizeMax) + 'px SimHei'
            let x = (i + 1) * (this.contentWidth / (this.identifyCode.length + 1))
            let y = this.randomNum(this.fontSizeMax, this.contentHeight - 5)
            //角度
            var deg = this.randomNum(-45, 45)
            //修改坐标原点和旋转角度
            ctx.translate(x, y)
            //弧度=角度*Math.PI/180;
            ctx.rotate(deg * Math.PI / 180)
            ctx.fillText(txt, 0, 0)
            //恢复坐标的原点和旋转角度
            ctx.rotate(-deg * Math.PI / 180)
            ctx.translate(-x, -y)
        },    
        //绘制干扰线
        drawLine (ctx) {
            for (let i = 0; i < 8; i++) {
            ctx.strokeStyle = this.randomColor(this.lineColorMin, this.lineColorMax)//绘制路径颜色
            ctx.beginPath()//开始一条路径
            ctx.moveTo(this.randomNum(0, this.contentWidth), this.randomNum(0, this.contentHeight))//移动到位置
            ctx.lineTo(this.randomNum(0, this.contentWidth), this.randomNum(0, this.contentHeight))//创建到达位置
            ctx.stroke()//进行绘制
            }
        },
        //绘制干扰点
        drawDot (ctx) {
            for (let i = 0; i < 100; i++) {
                ctx.fillStyle = this.randomColor(0, 255)//填充颜色
                ctx.beginPath()//开始一条路径
                //arc(x,y,半径r,起始角，结束角) 方法创建弧/曲线（用于创建圆或部分圆）。如需通过 arc() 来创建圆，请把起始角设置为 0，结束角设置为 2*Math.PI。
                ctx.arc(this.randomNum(0, this.contentWidth), this.randomNum(0, this.contentHeight), 1, 0, 2 * Math.PI)
                ctx.fill()//如果路径未关闭，那么 fill() 方法会从路径结束点到开始点之间添加一条线，以关闭该路径，然后填充该路径
            }
        }
    },
    watch: {
      identifyCode () {
        this.drawPic()
      }
    },
    mounted () {
      this.drawPic()
    }
}
</script> 

<style lang="stylus" scoped>
//  #yzm
    // width 300px
    // height 40px
    // margin 10px 45px
    // background-color yellow
    // .yzmimg
    //     height 40px
    //     line-height 40px
    //     width 100px
    //     float right 
.s-canvas
    display inline-block
    width 100px
    height 40px
</style>