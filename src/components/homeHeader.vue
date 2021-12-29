<template>
  <el-row class="header">
<!--    点击按钮控制左侧的menu缩进-->
    <el-col :span="2">
      <el-button type="info" icon="el-icon-menu" circle @click="changeMenu"></el-button>
    </el-col>
<!--    input框部分-->
    <el-col :span="9" :offset="3" class="inputBox">
      <el-input v-model="inputValue" :placeholder="lg.inputPlaceHolder" clearable class="inputSearch">
        <i slot="prefix" class="el-input__icon el-icon-search"></i>
        <el-button slot="append" icon="el-icon-search"></el-button>
      </el-input>
    </el-col>
<!--    帮助、关于、中英文切换-->
    <el-col class="userMessage" :span="6" :offset="4">
      <span class="spanBox">{{lg.help}}</span>
      <span class="spanBox">{{lg.about}}</span>
      <div class="lange" v-if="language=='english'" @click="changeLange">中</div>
      <div class="lange" v-else @click="changeLange">EN</div>
<!--      个人信息  头像及相关内容-->
      <div>
        <el-popover
          width="130"
          trigger="click">
          <div class="userSel">
            <div>{{lg.userMessage}}</div>
            <div>{{lg.loginOut}}</div>
          </div>
          <div class="userLogo" slot="reference">
            <img :src="logoImg" alt="">
            <div>
              <i class="el-icon-caret-bottom"></i>
            </div>
          </div>
        </el-popover>
      </div>
    </el-col>
  </el-row>
</template>
<script>
  export default {
      props:['lg'],
      name:'homeHeader',
      data(){
          return{
              // 左侧的开关
              value:true,
              // 输入的内容
              inputValue:'',
              // logo的路径
              logoImg:'http://120.27.243.181/image/dish/suancai.jpg',
              // 语言切换
              language:'chinese'
          }
      },
      methods:{
          // 控制左侧菜单
          changeMenu(){
              this.value = !this.value;
          },
          // 改变语言  传入到父组件
          changeLange(){
              if(this.language == 'chinese'){
                  this.language = 'english'
              }else{
                  this.language = 'chinese'
              }
              this.$emit("changeLang",this.language)
          }
      },
      watch:{
          value:function(newValue,oldValue){
              this.value = newValue;
              this.$emit("changeMenu",this.value)
          }
      }
  }
</script>
<style scoped>
  .header{
    height: 100%;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
  }
  .inputSearch{
    width: 100%;
  }
  .userLogo img{
    width: 40px;
    height: 40px;
    position: relative;
    overflow: hidden;
    border-radius: 50%;
    -webkit-border-radius:50%;
    -moz-border-radius:50%;
    margin-right: 5px;
  }
  .userLogo{
    display: flex;
    flex-direction: row;
    align-items: center;
  }
  .userMessage{
    display: flex;
    flex-direction: row;
    align-items: center;
  }
  .userMessage span{
    margin: 10px;
    cursor: pointer;
    color: #8d9a9c;
    font-size: 15px;
  }
  .userMessage span:hover{
    color: #125b70;
  }

  .lange{
    width: 40px;
    height: 40px;
    line-height: 40px;
    text-align: center;
    cursor: pointer;
    background: #fff;
    border-radius: 50%;
    margin: 0 10px;
  }
  .lange:hover{
    background: #f3f3f3;
  }


  .userSel{
    line-height: 30px;
  }
  .userSel div{
    cursor: pointer;
    color: #8d9a9c;
  }
  .userSel div:hover{
    color: #125b70;
  }

  @media screen and (max-width: 900px){
    .inputBox{
      display: none;
    }
    .spanBox{
      display: none;
    }
  }
</style>
