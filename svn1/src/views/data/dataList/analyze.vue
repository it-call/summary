<template>
    <div class="datalist1">
        <router-view></router-view>
        <div class="mychart" ref="echart"></div>
    </div>
</template>
<script>
    // 按需引入 引入 ECharts 主模块
    var echarts = require('echarts/lib/echarts');
    // 引入柱状图
    require('echarts/lib/chart/bar');
    // 引入提示框和标题组件
    require('echarts/lib/component/tooltip');
    require('echarts/lib/component/title');
    export default {
        data(){
            return {

            }
        },
        methods: {
            setOptions() {
                this.chart.setOption({
                    title: {
                    text: 'ECharts 入门示例'
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
                    }]
                })
            },
            initCharts() {
            this.chart = echarts.init(this.$refs.echart);
            this.setOptions();
            },
        },
        mounted(){
            this.initCharts();
            console.log(this.$refs,this.$el);
        },
    }
</script>
<style>
.setting{
    width:100%;
    height:100%;
    background:skyblue;
}
</style>