<template>
  <div class="login">
   <i class="el-icon-edit"></i>
    <el-form :model="ruleForm" status-icon :rules="rules" ref="ruleForm" class="demo-ruleForm">
      <el-form-item label="账号" prop="numVip">
        <el-input v-model.number="ruleForm.numVip" style="width:220px;"></el-input>
      </el-form-item>
      <el-form-item label="密码" prop="pass">
        <el-input type="password" v-model="ruleForm.pass" autocomplete="off" style="width:220px;"></el-input>
      </el-form-item>
      <el-form-item>
        <el-button type="primary" @click="submitForm('ruleForm')">登录</el-button>
        <el-button @click="add">注册</el-button>
      </el-form-item>
    </el-form>
  </div>
</template>

<script>
export default {
  name: "login",
  data() {
    var checkAge = (rule, value, callback) => {
      if (!value) {
        return callback(new Error("账号不能为空"));
      }
      if (value.toString().length < 5) {
        return callback(new Error("账号最少5位"));
      }
      callback();
    };
    var validatePass = (rule, value, callback) => {
      if (value === "") {
        callback(new Error("请输入密码"));
      }
      if (value.toString().length < 5) {
        value = "";
        return callback(new Error("密码最少5位"));
      }
      callback();
    };
    return {
      ruleForm: {
        pass: "",
        numVip: ""
      },
      rules: {
        pass: [{ validator: validatePass, trigger: "blur" }],
        numVip: [{ validator: checkAge, trigger: "blur" }]
      }
    };
  },
  methods: {
    submitForm(formName) {
      this.$refs[formName].validate(valid => {
        if (valid) {
          alert("submit!");
        } else {
          console.log("error submit!!");
          return false;
        }
      });
    },
    add() {
      console.log("跳转到注册页");
    }
  }
};
</script>

<style scoped>
.login {
  border: 1px solid lightgray;
  padding: 20px 0 0 30px;
  width: 300px;
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
}
</style>
