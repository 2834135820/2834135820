<template>
    <div class="animated bounceInRight">
      <div class="shop">

        <div class="shopBox" v-for="i in 12">
          <img src="../assets/image/milk.jpg" alt="">
          <div class="imgBottom">
            <div class="titleName">
              <span class="titleBox">{{lg.special}}</span>
              <span class="title">{{lg.shopName}}</span>
            </div>
            <div class="payButton">
              <span class="red">￥<span class="price">49.9</span></span>
              <el-button type="danger">
                {{lg.payNow}}
              </el-button>
            </div>

          </div>
        </div>

        <div class="choosePage">
          <el-pagination
            background
            layout="prev, pager, next"
            :total="50">
          </el-pagination>
        </div>


      </div>
    </div>
</template>

<script>
    export default {
        props:['activeMain','lg'],
        name: "commodityOverview",
        data(){
            return{
            }
        },
        created() {
        },
        methods:{
            readyData(){
            }
        },
        watch:{
            activeMain(){
            }
        }
    }
</script>

<style scoped>
  .shop{
    width: calc(100% - 20px);
    display: flex;
    flex-wrap: wrap;
    flex-direction: row;
    margin: 5px 10px;
  }
  .shopBox{
    width: calc(100% / 4 - 10px);
    background: #fff;
    border-radius: 5px;
    margin: 5px;
  }
  .shopBox img{
    width: calc(100% - 2px);
    border:1px solid #a9aeb0;
  }
  .titleName{
    display: flex;
    justify-content: space-between;
  }
  .title{
    font-weight: bold;
    font-size: 15px;
    color: #4c4c4a;
    display: -webkit-box;
    -webkit-box-orient: vertical;
    -webkit-line-clamp: 1;
    overflow: hidden;

  }
  .titleBox{
    background: #ff6a5a;
    color: #fff;
    font-size: 12px;
    padding: 2px 5px;
    border-radius: 3px;
  }
  .red{
    color: #ff0000;
  }
  .price{
    font-size: 25px;
    color: #ff0000;
  }
  .payButton{
    display: flex;
    flex-direction:row;
    justify-content: space-between;
    margin-top: 5px;
  }
  .imgBottom{
    padding: 0 15px 10px;
  }

  .choosePage{
    text-align: right;
    width: 100%;
    background: #fff;
    padding: 20px 0;
  }

  @media screen and (max-width: 900px){
    .shopBox{
      width: calc(100% / 1 - 10px);
      background: #fff;
      border-radius: 5px;
      margin: 5px;
    }
  }
</style>
