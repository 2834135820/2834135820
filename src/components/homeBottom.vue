<template>
    <div class="bottom">
      <img src="../assets/image/logo.png" alt="">
      <div>
        © {{lg.author}}：9322710658 | {{lg.mail}}：932271058@qq.com
      </div>
    </div>
</template>

<script>
    export default {
        props:['lg'],
        name: "homeBottom"
    }
</script>

<style scoped>
  .bottom{
    background: #d9dbda;
    text-align: center;
    width: calc(100% - 40px);
    height: 130px;
    padding: 40px 20px 0px;
    line-height: 40px;
  }
  .bottom img{
    width: 60px;
    height: 40px;
  }
  .bottom div{
    color: #7d7d7b;
    font-size: 12px;
  }
</style>
