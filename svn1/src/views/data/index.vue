<template>
  <div class="data">
    <Navbar/>
    <router-view></router-view>
    <div class="subnav">
      <span>车辆监控</span>
      <span>分析统计</span>
      <span>管理设置</span>
    </div>
    <div class="summary">
      <span>企业总数：</span>
      <span>车辆总数：</span>
      <span>车辆类型总数：</span>
      <span>车辆安装数：</span>
      <span>当前在线车辆数：</span>
    </div>
    <div class="chart"></div>
    <div class="chart"></div>
    <div class="chart"></div>
    <div class="chart"></div>
    <div class="chart"></div>
    <div class="chart"></div>
    <div class="chart"></div>
    <div class="footer">
      <span>企业视图</span>
      <span>疲劳驾驶分析</span>
      <span>车辆速度分析</span>
      <span>gps屏蔽分析</span>
      <span>告警分析</span>
      <span>车辆行驶位置分析</span>
      <span>交警查车统计</span>
    </div>
    <!-- <div class="data-left">
      <el-row class="tac">
        <el-col :span="3" class="daohang">
          <el-menu
            :default-active=activeIndex
            :default-openeds='openeds'
            class="el-menu-vertical-demo"
            @open="handleOpen"
            @close="handleClose"
            background-color="#545c64"
            text-color="#fff"
            active-text-color="#ffd04b"
          >
            <el-menu-item index="1">
              <i class="el-icon-menu"></i>
              <span slot="title" name="monitoring" @click="goto()">车辆监控</span>
            </el-menu-item>
            <el-menu-item index="2">
              <i class="el-icon-menu"></i>
              <span slot="title" name="analyze" @click="goto()">分析统计</span>
            </el-menu-item>
            <el-menu-item index="3">
              <i class="el-icon-document"></i>
              <span slot="title" name="setting" @click="goto()">管理设置</span>
            </el-menu-item>
          </el-menu>
        </el-col>
      </el-row>
    </div>
    <div class="data-right">
      <router-view></router-view>
      <div class="mychart" ref="echart"></div>
    </div> -->
  </div>    

</template>
<script>
import Navbar from '@/layout/components/Navbar';
// 按需引入 引入 ECharts 主模块
var echarts = require('echarts/lib/echarts');
// 引入柱状图
require('echarts/lib/chart/bar');
// 引入提示框和标题组件
require('echarts/lib/component/tooltip');
require('echarts/lib/component/title');
export default {
  // name: "data",
  data() {
    return {
      // title: "",
      // openeds: [],
      // activeIndex:3
    };
  },
  components:{
    Navbar
  },
  methods: {
    setOptions() {
        this.chart.setOption({
            title: {
            text: '柱形图'
            },
            tooltip: {},
            xAxis: {
            data: ["衬衫", "羊毛衫", "雪纺衫", "裤子", "高跟鞋", "袜子"]
            },
            yAxis: {},
            series: [{
            name: '销量',
            type: 'bar',
            data: [5, 20, 36, 10, 10, 20]
            }],
            // series : [
            //     {
            //         name: '访问来源',
            //         type: 'pie',
            //         radius: '55%',
            //         data:[
            //             {value:235, name:'视频广告'},
            //             {value:274, name:'联盟广告'},
            //             {value:310, name:'邮件营销'},
            //             {value:335, name:'直接访问'},
            //             {value:400, name:'搜索引擎'}
            //         ]
            //     }
            // ]
        })
    },
    initCharts() {
    this.chart = echarts.init(this.$refs.echart);
    this.setOptions();
    },
    // handleClick(tab, event) {
    //   console.log(tab, event);
    // },
    // handleOpen(key, keyPath) {
    //   console.log(key, keyPath ,'打开');
    //   this.openeds=keyPath;
      
    // },
    // handleClose(key, keyPath) {
    //   console.log(key, keyPath,'关闭');
    //     this.openeds=keyPath;
    // },
    // goto(name) {
    //   this.$router.push('/data/dataList'+{name});
    //   console.log(this.$router);
    // },
  },
  created() {
    // console.log(this.activeIndex,'默认索引');
    // $(".hamburger-container").hide();
    // console.log( this.$router.currentRoute);
    // if(this.$router.currentRoute.name=='dataList'){
    //   this.openeds=["1", "1-4"];
    //   this.activeIndex='1-4-1'
    // }else{
    //   this.openeds=[]
    //   this.activeIndex="2"
    // }
  },
  mounted(){
      $('.hamburger-container').hide();
      this.initCharts();
      // console.log(this.$refs,this.$el);
  },
}

</script>
<style lang="scss" scoped>
.data {
  width: 100%;
  height: auto;
  min-height: 200px; 
  // background-color: rgb(138, 211, 245);
  /* width: calc(100% - 210px); */
  .subnav{
    width: 100%;
    height: 40px;
    text-align: center;
    span{
      line-height: 40px;
      width: 100px;
      margin: 0 40px;
    }
  }
  .summary{
    width: 100%;
    height: 30px;
    text-align: center;
    span{
      line-height: 30px;
      width: 150px;
      margin: 0 30px;
    }
  }
  .chart{
    width: 100%;
    height: 300px;
    background-color: rgb(223, 37, 62);
  }
  .footer{
    width: 100%;
    height: 30px;
    text-align: center;
    span{
      line-height: 30px;
      width: 150px;
      margin: 0 30px;
    }
  }
}
</style>