<template>
  <div class="feedback">
    <div class="fd-title clearfix">
      <div class="fd1">
        支队：
        <el-input placeholder="请输入内容" v-model="input" clearable></el-input>
      </div>
      <div class="fd2">
        大队：
        <el-input placeholder="请输入内容" v-model="input" clearable></el-input>
      </div>
      <div class="fd3">
        约谈企业：
        <el-input placeholder="请输入内容" v-model="input" clearable class="fd3s"></el-input>
      </div>
    </div>
    <div class="main-text">
      &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;&nbsp; &nbsp;反馈内容：
      <div class="message">
        <el-input type="textarea" :rows="2" placeholder="请输入内容" v-model="textarea"></el-input>
      </div>
    </div>
    <div class="confirm">
         <el-button type="info" class="confirm-btn">确定</el-button>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      input: "",
      textarea: ""
    };
  }
};
</script>
<style scoped>
.feedback {
  width: 100%;
  height: 100%;
  background: skyblue;
  color:#4B7DC8;
}
.fd-title {
  width: 100%;
  height: 100px;
}
.fd1,
.fd2,
.fd3 {
  float: left;
  width: 350px;
  height: 100px;
  margin-left: 100px;
  line-height: 100px;
}
>>> .el-input {
  position: relative;
  left: 46px;
  top: -100px;
  font-size: 14px;
  display: inline-block;
  width: 87%;
}
.fd3s {
  position: relative;
  left: 80px;
}
.main-text {
  height: 500px;
  width: 100%;
  background: #edf5fb;
}
.message {
  width: 72.6%;
  height: 500px;
  margin-left: 143px;
  background: #58bc58;
  position: relative;
  top: -17px;
}
.el-textarea {
  width: 100%;
  height: 100% !important;
}
>>> .el-textarea__inner {
  height: 100%;
}
.confirm-btn{
    position:relative;left:43%;top:20px;
    width:100px;
}
</style>