<template>
  <div class="animated bounceInRight">
<!--    营业部分-->
    <div class="homeMenu">
      <div class="mainBox" v-for="item in menuMessage">
        <img :src="item.src" alt="">
        <div>
          <span class="mainBoxTitel">{{lg[item.name]}}：</span>
          <span class="mainBoxNum">{{item.value}}</span>
          <span class="mainBoxNum" v-if="item.key == 'piece'">{{lg.piece}}</span>
          <span class="mainBoxNum" v-if="item.key=='people'">{{lg.peopleNum}}</span>
          <span class="mainBoxNum" v-if="item.key=='money'">￥</span>
        </div>
      </div>
    </div>
<!--    卡片图表部分-->
    <div class="charts">
      <h1>{{lg.homeChartsTitle}}</h1>
      <ve-line  :data="chartData" :settings="chartSetting">
      </ve-line>
    </div>
<!--    卡片新闻部分-->
    <el-card>
      <div slot="header" class="clearfix">
        <span>{{lg.latestNews}}</span>
        <el-button style="float: right; padding: 3px 0" type="text">
          <el-tooltip :content="lg.share" placement="top">
            <i class="el-icon-share"></i>
          </el-tooltip>
        </el-button>
      </div>
      <div v-for="o in aboutMessage" class="newsBox text item">
        <span v-if="lang=='chinese'">{{o.chMessage}}</span>
        <span v-else>{{o.enMessage}}</span>
      </div>
    </el-card>
  </div>
</template>

<script>
  import VeLine from 'v-charts/lib/line'
  import homeData from "../assets/js/home";
    export default {
      props:['lg','lang'],
        name: "home",
        data(){
            return{
                dataObj:'',
                aboutMessage:'',
                menuMessage:"",
                chartData:"",
                chartSetting:""
            }
        },
        created() {
            this.chartSetting = {
                area: true
            }
            this.chartData = {
                columns: ['日期', '营业额' ,'利润'],
                rows: [
                    { '日期': '12-10', '营业额': 28605 ,'利润':"18300"},
                    { '日期': '12-11', '营业额': 23054.55 ,'利润':"11300" },
                    { '日期': '12-12', '营业额': 34650.44 ,'利润':"22300"},
                    { '日期': '12-13', '营业额': 28605.35 ,'利润':"17300"},
                    { '日期': '12-14', '营业额': 28605 ,'利润':"16300"},
                    { '日期': '12-15', '营业额': 23054.55 ,'利润':"10300" }
                ]
            }
            this.dataObj = homeData;
            this.aboutMessage = homeData.aboutMessage;
            this.menuMessage = homeData.menuMessage;
        },
        components:{
            VeLine
        }
    }
</script>

<style scoped>

  .homeMenu{
    width: 100%;
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
  }
  .mainBox{
    width: calc(25% - 20px);
    background: #fdfffe;
    border-radius: 5px;
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: left;
    margin:20px 5px;
    padding: 10px 5px;
    box-shadow: 2px 2px 10px #dcdcdc;
  }
  .mainBox img{
    width: 60px;
    height: 60px;
  }

  .mainBoxTitel{
    font-size: 18px;
    color: #737577;
  }
  .mainBoxNum{
    font-size: 14px;
    color: #b2b4b3;
  }
  .charts{
    width: calc(100% - 4px);
    background: #fff;
    margin:0px 2px 10px;
    text-align: center;
  }
  .charts h1{
    font-size: 25px;
    padding: 10px 0;
    font-weight: 400
  }
  .newsBox{
    line-height: 25px;
    text-decoration: underline;
    cursor: pointer;
    font-size: 16px;
    display: -webkit-box;
    -webkit-box-orient: vertical;
    -webkit-line-clamp: 1;
    overflow: hidden;
  }
  .newsBox:hover{
    color: #b2b4b3;
  }

  @media screen and (max-width: 900px){
    .mainBox{
      width: calc(100% - 20px);
      margin:5px 5px;
      padding: 10px 5px;
    }
  }
</style>
