<template>
    <div class="password">
      <el-form
        :model="ruleForm"
        :rules="rules"
        ref="ruleForm"
        label-position="left"
        label-width="0px"
      >
        <div class="title">
          <h3>找回密码</h3>
        </div>
        <!-- username -->
        <el-form-item prop="username">
          <el-input type="text" v-model="ruleForm.username" auto-complete="off" placeholder="账号">
            <i slot="prefix" class="fa fa-user-o"></i>
          </el-input>
        </el-form-item>

        <!-- email -->
        <el-form-item prop="email">
          <el-input type="text" v-model="ruleForm.email" auto-complete="off" placeholder="邮箱">
            <i slot="prefix" class="fa fa-envelope-o"></i>
          </el-input>
        </el-form-item>

        <!-- 确定 -->
        <el-form-item>
          <el-button
            @click.native.prevent="handleSubmit"
            :loading="loading"
            type="primary"
            style="width:100%;"
          >确定</el-button>
        </el-form-item>
      </el-form>
  </div>
</template>

<script>
import {unlogin} from '@/api/user'
    export default {
        name:'password',
        data(){
            return{
                loading:false,
                ruleForm:{
                    username:'',
                    email:'',
                 } ,
                 rules:{
                      username:[{required:true,message:"请输入账号",trigger:"blur"}],
                      email:[{required:true,message:"请输入邮箱地址",trigger:"blur"},
                            {type:"email",message:"请输入正确的邮箱地址",trigger:"blur"}]
                 }
            }
        },
        methods:{
            handleSubmit(){
                this.$refs["ruleForm"].validate((valid)=>{
                    if(valid){
                        this.loading=true;
                        unlogin().then(response=>{
                             this.loading=false;
                             console.log(response.data)
                        }).catch(()=>{
                            this.loading=false;
                        })
                    }
                })
            }
        }

    }
</script>

<style lang="scss" scoped>
.title {
  margin: 0px auto 40px auto;
  text-align: center;
  color: #505458;
}

i {
  font-size: 14px;
  margin-left: 8px;
}
</style>