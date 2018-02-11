<template>
<div class="t-login-body">
  <div class="t-login-frame">
    <div class="t-login-title">后台系统</div>
    <el-form :model="dynamicValidateForm" status-icon
             :rules="rules"
             ref="dynamicValidateForm" class="demo-dynamic">
      <el-form-item
        prop="email"
        :rules="[
      { required: true, message: '请输入邮箱地址', trigger: 'blur' },
      { type: 'email', message: '请输入正确的邮箱地址', trigger: 'blur,change' }
    ]"
      >
        <el-input v-model="dynamicValidateForm.email" placeholder="请随意输入邮箱"></el-input>
      </el-form-item>
      <el-form-item prop="pass">
        <el-input type="password" v-model="dynamicValidateForm.pass" placeholder="请随便输入密码"></el-input>
      </el-form-item>
      <el-form-item>
        <el-button type="primary" style="width: 100%" @click="submitForm('dynamicValidateForm')">提交</el-button>
      </el-form-item>
    </el-form>
  </div>

</div>
</template>

<script type="text/javascript">
export default {
  data () {
    let validatePass = (rule, value, callback) => {
      if (value === '') {
        callback(new Error('请输入密码'));
      } else {
        callback();
      }
    };
    return {
      dynamicValidateForm: {
        email: '',
        pass: ''
      },
      rules: {
        pass: [
          { validator: validatePass, trigger: 'blur' }
        ]
      }
    }
  },
  methods: {
    submitForm(formName) {
      this.$refs[formName].validate((valid) => {
        if (valid) {
          alert('成功!');
          this.$router.push({path: 'home'})
        } else {
          console.log('error submit!!');
          return false;
        }
      });
    }
  }
}
</script>

<style>
.t-login-body{
  position: fixed;
  width: 100%;
  height: 100%;
  background-color: #5fb0f5;
}
.t-login-frame{
  padding: 20px;
  position: fixed;
  left: 50%;
  top: 50%;
  margin-left: -200px;
  margin-top: -150px;
  width: 400px;
  height: 300px;
  background-color: white;
  border-radius: 8px;
}
.t-login-title{
  width: 100%;
  margin-bottom: 20px;
  font-size: 30px;
  color: #5fb0f5;
}
</style>
