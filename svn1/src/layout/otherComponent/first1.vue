<template>
  <div class="first1">
    <div class="maplist">
      <el-input placeholder="请输入内容" suffix-icon="el-icon-search" v-model="input2" class="mapSearch"></el-input>
      <!-- <el-autocomplete
        class="mapSearch"
        suffix-icon="el-icon-search"
        clearable
        v-model="mapLocation.address"
        :fetch-suggestions="querySearch"  
        placeholder="请输入内容"
        :trigger-on-focus="false"
        @select="handleSelect"
      />-->
      <el-tree
        :data="data"
        :props="defaultProps"
        accordion
        @node-click="handleNodeClick" 
        :load="loadNode"
        lazy
      >
      </el-tree>
      <!-- <svg-icon icon-class="bus" /> -->
    </div>
    <div class="mapdata">
      <baidu-map
        class="bm-view"
        :center="mapCenter"
        :zoom="mapZoom"
        :scroll-wheel-zoom="true"
        @ready="handlerBMap"
      />
      <div v-drag class="alert">
        <p>
          <i class="el-icon-edit"></i>&nbsp;速度
        </p>
        <p>
          <i class="el-icon-edit"></i>报警
        </p>
        <p>
          <i class="el-icon-edit"></i>状态
        </p>
        <p>
          <i class="el-icon-edit"></i>地址
        </p>
        <p>
          <i class="el-icon-edit"></i>经纬度
        </p>
        <p>
          <i class="el-icon-edit"></i>定位时间
        </p>
        <p>
          <i class="el-icon-edit"></i>视频回放
        </p>
        <p>
          <i class="el-icon-edit"></i>实时视频
        </p>
        <p>
          <i class="el-icon-edit"></i>语音播放
        </p>
      </div>
    </div>
  </div>
</template>
<script>
import { log } from "util";
export default {
  data() {
    return {
      input2: "",
      mapZoom: 15,
      mapCenter: { lng: 0, lat: 0 },
      mapLocation: {
        address: undefined,
        coordinate: undefined
      },
      carlist: [],
      data: [
       
      ],
      defaultProps: {
        children: "children",
        label: "label"
      }
    };
  },
  // 吴川的坐标：{lng: 110.78645, lat: 21.447263}
  mounted() {
    $(".hamburger-container").hide();
    const url = this.HOST + "/vehicle/getCompany";
    this.$axios.get(url, {}).then(res => {
      res.data.data.list.forEach(item => {
        this.carlist.push(item.name);
      });
      console.log("获取车辆信息", this.carlist);
      this.data = [];
      this.carlist.forEach(item => {
        this.data.push({
          label: item
       
        });
      });
    });
  },
  methods: {
    //加载第一级节点
    loadfirstnode(resolve, test) {
      console.log(test, "能传过来么");
      const url = this.HOST + "/vehicle/getCompany";
      this.$axios
        .get(url, {
          params: {
            name: test
          }
        })
        .then(res => {
          var name = res.data.data.list[0].name;
          var id = res.data.data.list[0].id;
          console.log("返回数据", name, id);
          var arr = [
            {
              label: id,
              icon: 'el-icon-info'
            },
            {
              label: name,
              icon: 'el-icon-info'
            }
          ];
          return resolve(arr);
        });
    },
    loadNode(node, resolve,event) {
      console.log(node, "这是什么");
      if (node.level == 1) {
        this.loadfirstnode(resolve, node.label);
      }else{
        resolve([])
      }
    },
    handleNodeClick(data) {
       console.log(data);
    },
    handlerBMap({ BMap, map }) {
      this.BMap = BMap;
      this.map = map;
      console.log("初始化");
      this.mapCenter.lng = 113.271429;
      this.mapCenter.lat = 23.135336;
      this.mapZoom = 10;
    },
    querySearch(queryString, cb) {
      console.log("cb参数是什么", cb);
    
    },
    handleSelect(item) {
      var { point } = item;
      console.log(item, 888);
      this.mapLocation.coordinate = point;
      console.log("经纬度？", point);
      this.makerCenter(point);
    },
    makerCenter(point) {
      if (this.map) {
        this.map.clearOverlays(); //清除地图的覆盖物
        this.map.addOverlay(new this.BMap.Marker(point)); //覆盖物红点添加到地图
        this.mapCenter.lng = point.lng;
        this.mapCenter.lat = point.lat;
        this.mapZoom = 15;
      }
    },
    test1() {
      $(".alert").show();
      this.makerCenter({ lng: 110.78645, lat: 21.447263 });
    }
  }
};
</script>
<style scoped>
>>> .el-tree-node__label {
  font-size: 14px;
  margin-left: 29px;
}
>>> .el-tree-node__content > .el-tree-node__expand-icon {
  padding: 6px;
  display: none;
}
.text {
  font-size: 14px;
}

.item {
  padding: 18px 0;
}

.box-card {
  width: 208px;
}
.el-card {
  border: none;
  height: calc(100% - 20px);
  overflow: auto;
}
.el-card.is-always-shadow,
.el-card.is-hover-shadow:focus,
.el-card.is-hover-shadow:hover {
  -webkit-box-shadow: none;
  box-shadow: none;
}
.first1 {
  width: 100%;
  height: calc(100% - 50px);
  background: #58bc58;
}
.map {
  width: 100%;
  height: 100%;
}
.maplist {
  width: 210px;
  height: 100%;
  background-color: #fff;
  position: fixed;
}
.mapdata {
  width: calc(100% - 210px);
  height: 100%;
  background: #58bc58;
  position: fixed;
  margin-left: 210px;
}
.mapSearch {
  position: relative;
  font-size: 14px;
  display: inline-block;
  width: 88%;
  margin-left: 11px;
  margin-top: 5px;
}
.bm-view {
  width: 100%;
  height: 100%;
}
.alert {
  width: 302px;
  height: 337px;
  background: #6e93c9;
  position: absolute;
  bottom: 200px;
  right: 100px;
  display: none;
}
.alert > p {
  padding-left: 30px;
  color: #ffff;
}
>>> .el-tree-node__content {
  height: 40px;
}
>>> .el-tree-node {
  white-space: normal;
  outline: 0;
}
</style>