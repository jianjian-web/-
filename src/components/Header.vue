<template>
  <div class="z-header">
    <span class='logo'>follow-up</span>
    <div class='rt'>
      <span class='btn login'>登录</span>
      <span class='btn bgColor'>注册</span>
    </div>
  </div>
</template>

<script>
export default {
  name: 'header',
  data () {
    return {
    }
  }
}
</script>

<style scoped lang=less>
@import url('../assets/css/base.less');
  .z-header{
    padding-left:22px;
    height: 60px;
    line-height: 60px;
    .logo{
      display: inline-block;
      width:160px;
      height: 36px;
      font-size:32px;
      font-weight: bold;
    }
    .rt{
      .btn{
        font-size:18px;
        padding:8px 31px;
        border:1px solid transparent;
        border-radius: 15px;
        cursor: pointer;
      }
      .login{
        color:#fff;
        border-color: #fff;
        margin-right:18px;
      }
      .bgColor{
        background-image: linear-gradient(225deg, #00ffff 0%, #7dffc9 45%, #faff93 100%);
      }
    }
  }
</style>
