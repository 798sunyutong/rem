<template>
<!-- <transition></transition>标签的作用https://blog.csdn.net/weixin_42218847/article/details/81474923 -->
<!-- 使用transition元素把需要被动画控制的元素，包裹起来；name区分不同组织间动画 -->
  <transition name="fade">
      <div class="toast" v-show="show">
      {{message}}
  </div>
  </transition>
</template>

<script>
export default {
    data() {
        return {
            show:false,
            message:''
        }
    },

}
</script>

<style lang="stylus" scoped>
.toast
    color red
    position fixed
    top 40%
    left 50%
    padding 15px
    min-width 300px
    font-size 28px
    text-align center
    background-color rgba(0,0,0,0.8)
    border-radius 8px
    z-index 10000
    transform translateX(-50%)
    -webkit-transform translateX(-50%)
    .fade-enter-active,
    .fade-leave-active
        transition 0.3s ease-out
    .fade-enter,
    .fade-leave-top 
        opacity 0
        transform scale(1)
</style>