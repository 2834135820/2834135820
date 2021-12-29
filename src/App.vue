<template>
<!--  页面加载效果-->
  <div id="app" v-loading="loading"
       element-loading-text="拼命加载中"
       element-loading-spinner="el-icon-loading"
       element-loading-background="rgba(0, 0, 0, 0.8)"
  >
<!--    内容部分-->
    <el-container style="height: 100%">
      <el-aside :width="leftWidth" class="leftHome">
<!--        左侧menu组件-->
        <leftHome @chooseMenu="chooseMenu" :activeMain="activeMain" :lg="lg" :isShow="isShow"></leftHome>
      </el-aside>
      <el-container>
        <el-header class="headerTop">
<!--          头部组件-->
          <homeHeader :lg="lg" @changeLang="changeLang" @changeMenu="changeMenu"></homeHeader>
        </el-header>
        <el-main class="home">
<!--          标签部分-->
<!--          首页标签-->
          <el-col class="breadBox">
            <el-tag
              effect="dark"
              class="breadIndex bread"
              @click="chooseTab('index')"
            >
              {{lg.index}}
            </el-tag>
<!--            增加的标签-->
            <el-tag
              :class="activeMain==tag?'bread activeMain':'bread'"
              :key="tag"
              v-for="tag in dynamicTags"
              closable
              :disable-transitions="false"
              @close="handleClose(tag)"
              @click="chooseTab(tag)"
            >
              {{lg[tag]}}
            </el-tag>
          </el-col>
<!--          内容组件-->
          <div class="homePageBox">
            <home :lg="lg" :lang="lang" v-if="activeMain=='index'"></home>
            <UserManage :lg="lg" :lang="lang" v-else-if="activeMain=='userManage'"></UserManage>
            <goodsSubmit :lg="lg" v-else-if="activeMain=='goodsSubmit'"></goodsSubmit>
            <commodityOverview
              :lg="lg"
              :activeMain="activeMain"
              v-else-if="activeMain=='milk'||activeMain=='commodity'||activeMain=='smoke'||activeMain=='cooking'||activeMain=='tools'"
            ></commodityOverview>
          </div>
          <homeBottom :lg="lg"></homeBottom>
        </el-main>
      </el-container>

    </el-container>
  </div>
</template>

<script>
  import homeHeader from "./components/homeHeader";
  import leftHome from "./components/leftHome";
  import chinese from "./assets/ch-ls/chinese";
  import english from "./assets/ch-ls/english"
  import home from "./components/home"
  import UserManage from "./components/UserManage"
  import commodityOverview from "./components/commodityOverview"
  import goodsSubmit from "./components/goodsSubmit"
  import homeBottom from "./components/homeBottom";

  export default {
      name:'app',
      data(){
          return{
              // 左侧的menu宽度
              leftWidth:'150px',
              // 左侧点击缩进
              isShow:true,
              // 中英文切换
              lg:chinese,
              lang:'chinese',
              // 是否显示加载效果
              loading:true,
              // tag组件的数组
              dynamicTags:[],
              // 当前打开的页面 默认为index
              activeMain:'index'
          }
      },
      components:{
          homeHeader,leftHome,home,UserManage,commodityOverview,goodsSubmit,homeBottom
      },
      created(){
          setTimeout(()=>{
              this.loading = false;
          },1000)
      },
      methods:{
          // 切换menu的显示隐藏
          changeMenu(msg){
              this.isShow = !this.isShow;
              if(!msg){
                  this.leftWidth = '60px'
              }else if(this.lg == english){
                  this.leftWidth = '250px'
              }else{
                  this.leftWidth = '160px'
              }

          },
          // 中英文切换
          changeLang(lang){
              this.loading = true;
              if(lang == 'chinese'){
                  if(this.isShow == true){
                      this.leftWidth = '160px'
                  }
                  this.lg = chinese
                  this.lang = 'chinese'
              }else{
                  if(this.isShow == true){
                      this.leftWidth = '250px'
                  }
                  this.lg = english;
                  this.lang = 'english'
              }
              setTimeout(()=>{
                  this.loading = false;
              },1000)
          },
          // 点击关闭tag标签
          handleClose(obj){
              if(obj == this.activeMain){
                  // 点击关闭当前标签时   主页自动变为前1个页面
                  if(this.dynamicTags.length == 1){
                      this.activeMain = 'index'
                  }else{
                      let name = this.dynamicTags[this.dynamicTags.indexOf(obj)-1]
                      this.activeMain = name;
                  }
              }
              this.dynamicTags.splice(this.dynamicTags.indexOf(obj),1);
          },
          // 点击左侧标签的回调方法
          chooseMenu(key){
              this.activeMain = key;
              if(this.dynamicTags.indexOf(key) >=0){

              }else if(key == "index"){

              }else{
                  this.dynamicTags.push(key)
              }
          },
          // 点击tag的方法
          chooseTab(key){
              //当前页面点击更改
              this.activeMain = key
          }
      },
      watch:{
          activeMain(){
              this.loading = true;
              setTimeout(()=>{
                  this.loading = false
              },1000)
          }
      }
  }
</script>

<style>
  *{
    font-family: "微软雅黑";
  }
html,body,#app{
  width: 100%;
  height: 100%;

}
  .leftHome{
    height: 100%;
    background: #125b70;
    color: #fff;
    transition: 0.2s linear;
  }
  .headerTop{
    background: #e1e9ff;
    color: #000;
  }
  .home{
    background: #f3f3f3;
    padding: 0px;
  }
  .breadBox{
    background: #f3f3f3;
    padding: 5px;
  }
  .breadIndex{
    width: 80px;
    text-align: center;
  }
  .bread{
    cursor: pointer;
    margin: 0 2px;
  }
  .homePageBox{
    width: 100%;
    margin-top: 50px;
  }
  .activeMain{
    background: #e0e2e0;
  }
</style>
