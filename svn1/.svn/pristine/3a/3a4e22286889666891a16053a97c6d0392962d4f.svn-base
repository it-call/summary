<template>
  <div class="version-container">
    <div class="search">
      全部：
      <el-radio v-model="radio" label="1" @change="test" />视频盒子：
      <el-radio v-model="radio" label="2" @change="test" />粤行盒子：
      <el-radio v-model="radio" label="3" @change="test" />
      <el-button type="primary" class="sear" @click="search()">查询</el-button>
    </div>
    <div class="car-title">
      <h4>车辆版本信息表</h4>
    </div>

    <div class="container_table">
      <el-table
        :data="
          tableData.slice((currentPage - 1) * pageSize, currentPage * pageSize)
        "
        style="width: 100%"
        :header-cell-style="headerStyle"
        stripe
        border
      >
        <el-table-column type="index" :index="indexMethod" width="80" label="序号" align="center" />
        <el-table-column
          prop="deviceClass"
          label="应用类别"
          width="160"
          align="center"
          :formatter="formatDeviceClass"
        />
        <el-table-column
          prop="type"
          width="150"
          label="版本类型"
          align="center"
          :formatter="formatType"
        />
        <el-table-column prop="versionName" width="160" label="版本名称" align="center" />
        <el-table-column prop="issueTime" width="200" label="发布时间" align="center" />
        <el-table-column prop="filePath" width="380" label="文件路径" align="center" />
        <el-table-column prop="fileSize" width="140" label="文件大小" align="center" />
        <el-table-column prop="count" width="140" label="当前版本设备数" align="center" />
        <!-- <el-table-column v-model="id" prop="id" label="ID" align="center" /> -->

        <el-table-column prop="id" label="安装车辆" align="center">
          <template slot-scope="scope">
            <el-button
              type="text"
              @click="
                dialogTableVisible = true;
                getGridData(scope.row);
              "
            >点击查看</el-button>
            <el-dialog
              title="当前版本设备列表"
              :visible.sync="dialogTableVisible"
              :modal-append-to-body="false"
            >
              <el-table :data="gridData" :header-cell-style="headerStyle" stripe border>
                <el-table-column type="index" label="序号" width="80" align="center" />
                <el-table-column property="licensePlate" label="车牌号码" width="140" align="center" />
                <el-table-column property="code" label="设备编码" width="320" align="center" />
                <el-table-column property="deviceSerial" label="设备序列号" width="240" align="center" />
                <el-table-column
                  property="state"
                  label="设备状态"
                  align="center"
                  :formatter="formatState"
                />
              </el-table>
            </el-dialog>
          </template>
        </el-table-column>
      </el-table>
    </div>

    <el-pagination
      class="fy"
      layout="total, prev, pager, next, jumper"
      :total="total"
      :current-page.sync="activePage"
      @current-change="current_change"
      @size-change="handleSizeChange"
    />

    <div class="add">
      <el-button type="primary" class="add-btn" @click="dialogFormVisible = true">添加</el-button>
      <el-dialog title="添加版本信息" :visible.sync="dialogFormVisible">
        <el-form :model="form">
          <el-form-item label="设备类型">
            <el-select v-model="form.deviceClass" placeholder="请选择应用类别">
              <el-option label="devVerGw" value="1" />
              <el-option label="devVerH6" value="2" />
            </el-select>
          </el-form-item>
          <el-form-item label="版本类型">
            <el-select v-model="form.type" placeholder="请选择版本类型">
              <el-option label="主版本" value="1" />
              <el-option label="子版本" value="2" />
            </el-select>
          </el-form-item>
          <el-form-item label="版本名称">
            <el-input v-model="form.versionName" />
          </el-form-item>

          <el-form-item label="上传文件">
            <input
              ref="inputFile"
              class="file uploadinput"
              type="file"
              accept="image/png, image/gif, image/jpeg"
              @change="inputFileChange"
            >
          </el-form-item>
        </el-form>
        <div slot="footer" class="dialog-footer">
          <el-button @click="dialogFormVisible = false">取 消</el-button>
          <el-button
            type="primary"
            @click="
              dialogFormVisible = false;
              addInfo();
            "
          >确 定</el-button>
        </div>
      </el-dialog>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      // 分页
      radio: '1',
      total: 0, // 默认数据总数
      pageSize: 10, // 每页的数据条数
      currentPage: 1, // 默认开始页面
      istag: true,
      input: '',
      activePage: 1, // 当前显示页面

      dialogTableVisible: false,
      dialogFormVisible: false,
      fileList: '',

      tableData: [],
      deviceClass: '',
      versionId: '',

      gridData: [],

      form: {
        deviceClass: '1',
        type: '1',
        file: '',
        versionName: ''
      }
    }
  },

  updated() {
    // console.log(this.radio)
  },
  created() {
    this.getData()
    // console.log(this.tableData, 'created测试')
  },
  mounted() {
    this.getData()
    this.total = this.tableData.length
    // console.log(this.tableData, 'mounted测试')
    // console.log(this.total, '测试total')
  },

  methods: {
    test(x) {
      console.log('触发事件', x)
    },
    handleSizeChange(val) {
      console.log(`每页 ${val} 条`)
      this.pageSize = val
    },
    handleCurrentChange(val) {
      console.log(`当前页: ${val}`)
      this.currentPage = val
    },
    current_change: function(currentPage) {
      this.currentPage = currentPage
    },

    // 解决索引只排序当前页的问题,增加函数自定义索引序号
    indexMethod(index) {
      return (this.activePage - 1) * this.pageSize + index + 1
    },
    headerStyle() {
      return 'background:#B0BBD2FF';
    },
    search: function() {
      this.activePage = 1
      this.currentPage = 1

      if (this.radio === '2') {
        this.deviceClass = '1';
      } else if (this.radio === '3') {
        this.deviceClass = '2';
      } else {
        this.deviceClass = '';
      }
      this.getData()
    },

    inputFileChange(e) {
      // input的@change事件拿到数据
      this.fileList = e.target.files[0]
      console.log(this.fileList)
      this.form.versionName = e.target.files[0].name
    },
    addInfo() {
      // const qs = require('qs')
      var url = this.HOST + '/firmware/issueVersion';
      console.log(url)
      const data = new FormData()
      data.append('deviceClass', this.form.deviceClass)
      data.append('type', this.form.type)
      data.append('versionName', this.form.versionName)
      data.append('file', this.fileList)
      console.log(this.fileList)

      this.$axios
        .post(url, data, { headers: { 'Content-Type': 'multipart/form-data' }})
        .then(res => {
          console.log(res)
          this.search()
        })
        .catch(error => {
          console.log(error)
        })
      // this.tableData.unshift()

      // console.log(this.tableData, '新增数据')
    },
    getData() {
      const url = this.HOST + '/firmware/getVersionList/0/0/';
      console.log(url)
      this.$axios
        .get(url, {
          params: {
            deviceClass: this.deviceClass
          }
        })
        .then(res => {
          // console.log(res.data.data)
          this.tableData = res.data.data.list
          // console.log(this.tableData, '测试获取数据=' + this.deviceClass)
          this.total = this.tableData.length

          // 每次默认显示第一页
          // this.currentPage = 1
          this.activePage = 1

          // console.log(Math.ceil(this.total / this.pageSize), '测试总页数')
        })
        .catch(error => {
          console.log(error)
        })
    },
    formatDeviceClass(val) {
      if (val.deviceClass === 1) {
        return 'devVerGw';
      } else {
        return 'devVerH6';
      }
    },
    formatType(val) {
      if (val.type === 1) {
        return '主版本';
      } else {
        return '子版本';
      }
    },
    formatState(val) {
      if (val.state === 1) {
        return '离线';
      } else if (val.state === 2) {
        return '在线';
      } else {
        return '注册';
      }
    },
    getGridData(val) {
      // console.log(val.id, '测试当前数据id')
      this.versionId = val.id
      const url = this.HOST + '/firmware/getDeviceList/0/0/';
      // console.log(url)
      this.$axios
        .get(url, {
          params: {
            versionId: this.versionId
          }
        })
        .then(res => {
          // console.log(res.data.data)
          this.gridData = res.data.data.list
          // console.log(this.gridData, '测试获取当前版本车辆数据')
        })
        .catch(error => {
          console.log(error)
        })
    }
  }
}
</script>

<style scoped>
.version-container {
  background: #edf5fb;
  padding: 20px;
}
.line {
  text-align: center;
}
.search {
  line-height: 100px;
  box-sizing: border-box;
  /* paddsing-left: 30px; */
}
>>> .el-radio__label {
  display: none;
}
.sear {
  width: 90px;
  margin-left: 50px;
}
.car-title {
  width: 100%;
  height: 50px;
  text-align: center;
  font-weight: 400;
  color: rgba(92, 158, 255, 1);
}
.main {
  /* width: 100%;
  min-height: 600px; */
  padding-bottom: 60px;
}
.fy {
  /* position: relative; */
  margin: 30px 0;
  text-align: center;

  /* filepath: relative;
  left: 90%;
  bottom: -5%;
  transform: translate(-50%, -65%); */
}
.add {
  width: 100%;
  height: 100px;
}
.add-btn {
  width: 102px;
  height: 34px;
  color: rgba(255, 255, 255, 1);
  line-height: 8px;
  text-align: center;
}
.uploadinput {
  line-height: 200%;
}
.el-dialog__header {
  text-align: center;
}
</style>
<style>
.version-container .el-table th > .cell {
  color: #fff;
}
.version-container
  .el-table--striped
  .el-table__body
  tr.el-table__row--striped
  td {
  background: #f2f2f2;
}
.version-container .el-table td {
  padding: 0 0;
}
.version-container .el-dialog .el-table td {
  padding: 6px 0;
}
.version-container
  .el-dialog
  .el-table--striped
  .el-table__body
  tr.el-table__row
  td {
  background: unset;
}
.version-container
  .el-dialog
  .el-table--striped
  .el-table__body
  tr.el-table__row--striped
  td {
  background: #f2f2f2;
}
</style>
