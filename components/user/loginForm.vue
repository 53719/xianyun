<template>
  <el-form :model="form" ref="form" :rules="rules" class="form">
    <!-- 新增了prop属性 -->
    <el-form-item class="form-item" prop="username">
      <el-input placeholder="用户名/手机" v-model="form.username" @focus="hideErrMsg('username')"></el-input>
    </el-form-item>

    <!-- 新增了prop属性 -->
    <el-form-item class="form-item" prop="password">
      <el-input placeholder="密码" type="password" v-model="form.password"></el-input>
    </el-form-item>

    <p class="form-text">
      <nuxt-link to="#">忘记密码</nuxt-link>
    </p>

    <el-button class="submit" type="primary" @click="handleLoginSubmit">登录</el-button>
  </el-form>
</template>

<script>
export default {
  data() {
    return {
      // 表单数据
      form: {
        // 登录用户名/手机
        username: "",
        // 登录密码
        password: ""
      },
      // 表单规则
      rules: {
        rules: {
          username: [
            {
              required: true,
              message: "请输入用户名",
              trigger: "blur"
            },
            {
              min: 6,
              max: 15,
              message: "用户名在 6 到 15 个字符之间",
              trigger: "blur"
            },
            // 还可以使用正则表达式
            {
              pattern: /^\d+$/,
              message: "用户名只能输入数字",
              trigger: "blur"
            }
          ],
          password: [
            {
              required: true,
              message: "请输入密码",
              trigger: "blur"
            },
            // 效验属性本身是一个数组
            // 数组里面有规则对象
            // 规则对象可以不止有一个
            {
              pattern: /^\d{5,8}$/,
              message: "密码是五到八位的数字组成",
              trigger: "blur"
            }
          ]
        }
      }
    };
  },
  methods: {
    //   测试账号
    //   账号：13800138000
    //   密码：123456
    // 提交登录
    handleLoginSubmit() {
      //   验证表单
      this.$refs["form"].validate(valid => {
        //为true表示没有错误
        if (valid) {
          this.$axios({
            url: "/accounts/login",
            method: "POST",
            data: this.form
          }).then(res => {
            console.log(res.data);
          });
        }
      });
    },
    //清理表单方法
    hideErrMsg(propName) {
      this.$refs.form.clearValidate(propName);
    }
  }
};
</script>

<style scoped lang="less">
.form {
  padding: 25px;
}

.form-item {
  margin-bottom: 20px;
}

.form-text {
  font-size: 12px;
  color: #409eff;
  text-align: right;
  line-height: 1;
}

.submit {
  width: 100%;
  margin-top: 10px;
}
</style>