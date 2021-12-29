<template>
  <div class="animated bounceInRight">
    <el-table :data="tableData" class="tableBox">
      <el-table-column
        type="index">
      </el-table-column>
      <el-table-column prop="date" :label="lg.date"></el-table-column>
      <el-table-column :prop="lang=='chinese'?'name':'enName'" :label="lg.userName"></el-table-column>
      <el-table-column :prop="lang=='chinese'?'adress':'engAdress'" :label="lg.address"></el-table-column>
      <el-table-column prop="point" :label="lg.point"></el-table-column>
      <el-table-column :label="lg.operation">
        <template slot-scope="scope">
          <el-button
            size="mini" icon="el-icon-edit" @click="openMessage(1)">{{lg.edit}}</el-button>
          <el-button
            size="mini"
            type="danger" icon="el-icon-delete" @click="openMessage(2)">{{lg.delete}}</el-button>
        </template>
      </el-table-column>
    </el-table>
    <div class="choosePage">
      <el-pagination
        background
        layout="prev, pager, next"
        :total="50">
      </el-pagination>
    </div>
  </div>
</template>

<script>
  import userData from "../assets/js/user";
    export default {
      props:['lg','lang'],
        name: "UserManage",
        data(){
            return{
                tableData:[]
            }
        },
        created() {
            this.tableData = userData.data;
        },
        methods:{
            openMessage(num){
                switch (num) {
                    case 1:
                        this.$message("你点击了编辑")
                        break;
                    case 2:
                        this.$message({
                            message:"你点击了删除",
                            type:"warning"
                        })
                        break;
                }
            }
        }
    }
</script>

<style scoped>
  .tableBox{
    width: calc(100% - 10px);
    margin: 5px;
  }
  .choosePage{
    text-align: right;
    width: 100%;
    background: #fff;
    padding: 20px 0;
  }
</style>
