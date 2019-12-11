<template>
  <div class="datalist2">
    <router-view></router-view>
    <div class="title">
      车牌号码:
      <span class="input1">
        <el-input v-model="input" placeholder="请输入内容"></el-input>
      </span>
      <span class="input2">
        <el-select v-model="value" placeholder="请选择">
          <el-option v-for="item in options" :key="item.value" :label="item.label" :value="item.value" ></el-option>
        </el-select>
      </span>
      <span class="input3">
        <el-select v-model="value" placeholder="请选择">
          <el-option v-for="item in options" :key="item.value" :label="item.label" :value="item.value" ></el-option>
        </el-select>
      </span>
      起止日期：
      <el-date-picker
        v-model="model.starttime"
        type="datetime"
        placeholder="选择日期时间"
        :picker-options="startTime"
        @change="chooseTimeRange"
        value-format="yyyy-MM-dd HH:mm:ss"
      ></el-date-picker>至
      <el-date-picker
        v-model="model.endtime"
        type="datetime"
        placeholder="选择日期时间"
        :picker-options="endTime"
        @change="chooseTimeRange1"
        value-format="yyyy-MM-dd HH:mm:ss"
      ></el-date-picker>日期：
      <span class="input4">
        <el-select v-model="value" placeholder="请选择">
          <el-option
            v-for="item in options"
            :key="item.value"
            :label="item.label"
            :value="item.value"
          ></el-option>
        </el-select>
      </span>
      <span class="input5">
        <el-button type="success">确定</el-button>
      </span>
    </div>
    <div class="echart" id="echart"></div>
    <div class="table">
      <div class="table-title">
        <el-button type="success" class="table-button">统计图</el-button>
        <el-button type="success" class="table-button">统计表</el-button>
      </div>
      <div class="table-main">
        <template>
          <el-table
            :data="tableData"
            class="main"
            :header-cell-style="headClass"
            border
            style="width: 60%"
          >
            <el-table-column prop="date" label="序号" width="180"></el-table-column>
            <el-table-column prop="name" label="名称" width="180"></el-table-column>
            <el-table-column prop="address" label="总数"></el-table-column>
            <el-table-column prop="address" label="不规范安装"></el-table-column>
            <el-table-column prop="address" label="规范安装"></el-table-column>
            <el-table-column prop="address" label="规范使用次数"></el-table-column>
          </el-table>
        </template>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      options: [
        {
          value: "选项1",
          label: "80"
        },
        {
          value: "选项2",
          label: "90"
        },
        {
          value: "选项3",
          label: "100"
        },
        {
          value: "选项4",
          label: "110"
        },
        {
          value: "选项5",
          label: "120"
        }
      ],
      tableData: [
        {
          date: "2016-05-02",
          name: "王小虎",
          address: "上海市普陀区"
        },
        {
          date: "2016-05-04",
          name: "王小虎",
          address: "上海市普陀区"
        },
        {
          date: "2016-05-01",
          name: "王小虎",
          address: "上海市普陀区"
        },
        {
          date: "2016-05-03",
          name: "王小虎",
          address: "上海市普陀区"
        }
      ],
      value: "记录仪速度",

      input: "",
      model: {
        starttime: "",
        endtime: ""
      },
      /* start 开始时间小于今天,结束时间不能大于开始时间 */
      startTime: {
        disabledDate: time => {
          if (this.endtime) {
            return time.getTime() > new Date(this.endtime).getTime();
          } else {
            return time.getTime() > Date.now();
          }
        }
      },
      endTime: {
        disabledDate: time => {
          if (this.model.starttime) {
            return (
              time.getTime() > Date.now() ||
              time.getTime() < new Date(this.model.starttime).getTime()
            );
          } else {
            return time.getTime() > Date.now();
          }
        }
      }
    };
  },
  methods: {
    headClass() {
      return "background:#FFB8DFFC";
    },
    chooseTimeRange(t) {
      console.log(t);
      this.start_time = t;
    },
    chooseTimeRange1(t) {
      console.log(t);
      this.end_time = t;
    },
    creatEcharts() {
      let myEchart = this.$echarts.init(document.getElementById("echart"));
      console.log(myEchart);
      myEchart.setOption({
        xAxis: {
          type: "category",
          data: ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"]
        },
        yAxis: {
          type: "value"
        },
        series: [
          {
            data: [820, 932, 901, 934, 1290, 1330, 1320],
            type: "line"
          }
        ]
      });
    }
  },
  watch: {
    start_time(newval, oldval) {
      console.log(newval, "新的时间");
      this.start_time = newval;
    },
    end_time(newval) {
      this.end_time = newval;
    }
  },
  mounted() {
    this.creatEcharts();
  }
};
</script>
<style>
.datalist2 {
  width: 100%;
  height: 100%;
}
.title {
  width: 100%;
  height: 100px;
  box-sizing: border-box;
  padding-left: 20px;
  /* padding-top: 20px; */
  line-height: 100px;
}
.input1 {
  display: inline-block;
  width: 118px;
  height: 50px;
}
.input2 {
  display: inline-block;
  width: 118px;
  height: 50px;
  margin-left: 20px;
  color: #ffffff;
}
.input3 {
  display: inline-block;
  width: 88px;
  height: 50px;
  margin-left: 20px;
  color: #ffffff;
}
.input4 {
  display: inline-block;
  width: 118px;
  height: 50px;
  margin-left: 20px;
  color: #ffffff;
}
.input5 {
  display: inline-block;
  width: 118px;
  height: 50px;
  margin-left: 20px;
  color: #ffffff;
}
.echart {
  width: 100%;
  height: 300px;
  background: #fff;
}
.table {
  width: 100%;
  height: 400px;
}
.table-title {
  width: 100%;
  height: 50px;
  line-height: 50px;
  box-sizing: border-box;
  padding-left: 20px;
}
.table-button {
  width: 70px;
  height: 30px;
  text-align: center;
  font-size: 16px;
  line-height: 6px;
  padding-left: 9px;
}
.table-button > span {
  width: 70px;
  height: 30px;
}
.table-main {
  width: 100%;
  height: 300px;
}
.main {
  margin-left: 20px;
}

.has-gutter {
  background: blue !important;
}
</style>