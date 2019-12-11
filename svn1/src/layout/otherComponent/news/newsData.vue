<template>
    <div class="newsdata">
    
    <div class="data-left">
         <el-row class="tac">
        <el-col :span="12" class="daohang">
          <el-menu
            class="el-menu-vertical-demo"
            @open="handleOpen"
            @close="handleClose"
            background-color="#545c64"
            text-color="#fff"
            active-text-color="#ffd04b"
          >
            <el-menu-item index="2">
              <i class="el-icon-menu"></i>
              <span slot="title" @click='feedback'>消息反馈</span>
            </el-menu-item>
            <el-menu-item index="3">
              <i class="el-icon-document"></i>
              <span slot="title">消息推送</span>
            </el-menu-item>
          </el-menu>
        </el-col>
      </el-row>
    </div>
    <div class="data-right">
            <router-view></router-view>
    </div>
    </div>
</template>
<script>
import { log } from 'util';

export default{
    data(){
        return{

        }
    },
    methods:{
         handleOpen(key, keyPath) {
        console.log(key, keyPath);
      },
      handleClose(key, keyPath) {
        console.log(key, keyPath);
      },
      feedback(){
        
        this.$router.push('/news/newdata/feedback')
          // console.log(this.$router.push);
      }
    },
    mounted(){
           $('.hamburger-container').hide();  
        //    console.log(this.$router.currentRoute.name,'1111');
           
    }
    
}
</script>
<style scoped>
.newsdata{
    width:100%;
    height:calc(100% - 50px);
    background: blue;
}
.data-left{
     width: 210px;
  position: fixed;
  height: 100%;
  background-color: rgb(84, 92, 100);
}
.data-right{
     width: calc(100% - 210px);
  height: 100%;
  background: #58bc58;
  position: fixed;
  margin-left: 210px;
}
.daohang {
  width: 101%;
  height: 100%;
}
</style>