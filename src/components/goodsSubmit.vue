<template>
    <div class="animated bounceInRight">
      <el-form ref="form" :model="form" label-width="160px" class="formBox">
        <el-form-item :label="lg.goodsName">
          <el-input v-model="form.name"></el-input>
        </el-form-item>
        <el-form-item :label="lg.serviceArea">
          <el-select v-model="form.region" :placeholder="lg.chooseArea">
            <el-option :label="lg.shopOne" value="shanghai"></el-option>
            <el-option :label="lg.shopTwo" value="beijing"></el-option>
          </el-select>
        </el-form-item>
        <el-form-item :label="lg.goodsTime">
          <el-col :span="12">
            <el-date-picker type="date" :placeholder="lg.chooseDate" v-model="form.date1" style="width: 100%;"></el-date-picker>
          </el-col>
          <el-col :span="12">
            <el-time-picker :placeholder="lg.chooseTime" v-model="form.date2" style="width: 100%;"></el-time-picker>
          </el-col>
        </el-form-item>
        <el-form-item :label="lg.delivery">
          <el-switch v-model="form.delivery"></el-switch>
        </el-form-item>
        <el-form-item :label="lg.goodsScope">
          <el-checkbox-group v-model="form.type">
            <el-checkbox :label="lg.milk" name="type"></el-checkbox>
            <el-checkbox :label="lg.commodity" name="type"></el-checkbox>
            <el-checkbox :label="lg.smoke" name="type"></el-checkbox>
            <el-checkbox :label="lg.cooking" name="type"></el-checkbox>
            <el-checkbox :label="lg.tools" name="type"></el-checkbox>
          </el-checkbox-group>
        </el-form-item>
        <el-form-item :label="lg.payType">
          <el-radio-group v-model="form.resource">
            <el-radio :label="lg.payOnline"></el-radio>
            <el-radio :label="lg.payOffline"></el-radio>
          </el-radio-group>
        </el-form-item>
        <el-form-item :label="lg.remake">
          <el-input type="textarea" v-model="form.desc"></el-input>
        </el-form-item>
        <el-form-item>
          <el-button type="primary" @click="onSubmit">{{lg.goodsCreate}}</el-button>
          <el-button>{{lg.back}}</el-button>
        </el-form-item>
      </el-form>
    </div>
</template>

<script>
    export default {
        props:['lg'],
        name: "goodsSubmit",
        data(){
            return{
                form: {
                    name: '',
                    region: '',
                    date1: '',
                    date2: '',
                    delivery: false,
                    type: [],
                    resource: '',
                    desc: ''
                }
            }
        },
        created() {
        },
        methods:{
            onSubmit(){
                this.$message("你点击了创建")
            }
        }
    }
</script>

<style scoped>
.formBox{
  width: 90%;
  padding: 10px 5%;
}
</style>
