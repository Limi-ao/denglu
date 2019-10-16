<template>
  <div class="container">
    <el-input-number v-model="addNum" :min="1" :max="10" label="描述文字" />
    <el-input-number v-model="delNum" :min="1" :max="10" label="描述文字" /><br>
    <el-badge :value="time" :max="5"><el-button v-waves type="primary" @click="getIconsData">更新位置</el-button></el-badge>
    <el-button v-waves type="primary" @click="getListData">更新数据</el-button>
    <div class="bg">
      <svg-icon v-for="(icon,index) in icons" :key="index" :icon-class="icon.src" size="small" :style="{cursor:'pointer',color:'#fff',position:'absolute',left:icon.left+'%',top:icon.top+'%'}" @click="clickIcon(icon)" />
    </div>
    <div class="bg2">
      <svg-icon v-for="(icon,index) in icons" :key="index" :icon-class="icon.src" size="small" :style="{cursor:'pointer',color:'#fff',position:'absolute',left:icon.left+'%',bottom:icon.top+'%'}" @click="clickIcon(icon)" />
    </div>
    <div class="bg">
      <svg-icon v-for="(icon,index) in icons" :key="index" :icon-class="icon.src" size="small" :style="{cursor:'pointer',color:'#fff',position:'absolute',left:icon.left+'%',top:icon.top+'%'}" @click="clickIcon(icon)" />
    </div>
    <div class="bg2">
      <svg-icon v-for="(icon,index) in icons" :key="index" :icon-class="icon.src" size="small" :style="{cursor:'pointer',color:'#fff',position:'absolute',left:icon.left+'%',top:80-icon.top+'%'}" @click="clickIcon(icon)" />
    </div>
    <el-table
      ref="multipleTable"
      :data="listData"
      tooltip-effect="dark"
      style="width: 60%;margin:0 auto"
      @selection-change="handleSelectionChange"
      @row-click="selectRowClick"
    >
      <el-table-column
        type="selection"
        width="55"
      />
      <el-table-column
        prop="name"
        label="姓名"
        width="120"
      >
        <!-- <template slot-scope="scope">{{ scope.row.name }}</template> -->
      </el-table-column>
      <el-table-column
        prop="sex"
        label="性别"
        width="120"
      />
      <el-table-column
        prop="age"
        label="年龄"
        width="120"
      />
      <el-table-column
        prop="address"
        label="地址"
        show-overflow-tooltip
      />
    </el-table>
    <el-pagination
      style="width:60%;margin:0 auto;padding-bottom:30px"
      :current-page="currentPage"
      :page-sizes="[10, 50, 100]"
      :page-size="10"
      layout="total, sizes, prev, pager, next, jumper"
      :total="total"
      @size-change="handleSizeChange"
      @current-change="handleCurrentChange"
    />
  </div>
</template>

<script>
import axios from 'axios'
import waves from '@/directive/waves/index.js' // 水波纹指令
export default {
  name: 'Counter',
  directives: {
    waves
  },
  data() {
    return {
      addNum: 1,
      delNum: 1,
      time: 0,
      currentPage: 1,
      total: 400,
      icons: [
      ],
      bts: [],
      listData: [],
      selectedRows: []
    }
  },
  mounted() {
    this.getIconsData()
    this.getListData()
  },
  // activated() {
  //   if (!this.icons.length) {
  //     this.getIconsData()
  //   }
  // },
  // deactivated() {
  //   if (!this.icons.length) {
  //     this.getIconsData()
  //   }
  // },
  methods: {
    getIconsData() {
      this.time = this.time + 1
      axios.get('https://www.easy-mock.com/mock/5d1c63ad5a92b35a16acf307/base').then(res => {
        if (res.status === 200) {
          this.icons = res.data.data
        }
      }).catch(e => {
        console.log(e)
        this.icons = [{ 'icon': 'el-icon-view', 'left': 30.4, 'src': 'wechat', 'top': 78.7, 'id': 10001 }, { 'icon': 'el-icon-odometer', 'left': 76.7, 'src': 'eye', 'top': 60.5, 'id': 10002 }, { 'icon': 'el-icon-first-aid-kit', 'left': 66.5, 'src': 'peoples', 'top': 30.3, 'id': 10003 }, { 'icon': 'el-icon-view', 'left': 53.8, 'src': 'wechat', 'top': 37.7, 'id': 10004 }, { 'icon': 'el-icon-view', 'left': 71.7, 'src': 'wechat', 'top': 37.8, 'id': 10005 }, { 'icon': 'el-icon-caret-top', 'left': 78.4, 'src': 'bug', 'top': 70.1, 'id': 10006 }, { 'icon': 'el-icon-caret-right', 'left': 13.5, 'src': 'password', 'top': 73.4, 'id': 10007 }, { 'icon': 'el-icon-caret-top', 'left': 57.9, 'src': 'star', 'top': 60.4, 'id': 10008 }, { 'icon': 'el-icon-discover', 'left': 54.5, 'src': 'qq', 'top': 17.6, 'id': 10009 }, { 'icon': 'el-icon-discover', 'left': 50.1, 'src': 'eye-open', 'top': 8.5, 'id': 10010 }]
        this.$swal({
          type: 'error',
          title: '失败',
          showCloseButton: true,
          text: e.message
        })
      })
    },
    getListData() {
      axios.get('https://www.easy-mock.com/mock/5d1c63ad5a92b35a16acf307/mulTable', { params: { currentPage: this.currentPage }}).then(res => {
        if (res.status === 200) {
          this.listData = res.data.data
        }
      }).catch(e => {
        this.$swal({
          type: 'error',
          title: '请求失败',
          showCloseButton: true,
          text: e.message
        })
      })
    },
    handleSelectionChange(row) {
      this.selectedRows = row
    },
    selectRowClick(row) {
      this.$refs.multipleTable.toggleRowSelection(row)
    },
    handleCurrentChange(currentPage) {
      this.currentPage = currentPage
      this.getListData()
    },
    handleSizeChange(size) {
      this.size = size
      this.getListData()
    },
    clickIcon(icon) {
      this.$swal({
        type: 'success',
        title: '点击成功',
        customClass: {
          title: 'successAlert'
        },
        showCloseButton: true,
        text: `你点击了id为${icon.id}的图标,类型为${icon.src},当前位置${icon.left},${icon.top}`
      })
    }
  }
}
</script>

<style scoped>
.container{
  margin:0 auto;
}
.bg{
  background: #0099ff;
  margin: 0 auto;
  margin-top: 30px;
  position: relative;
  width: 1000px;
  height:150px;
}
.bg2{
  background: #0099ff;
  margin: 0 auto;
  margin-top: 5px;
  position: relative;
  width: 1000px;
  height:150px;
}
.el-button+.el-button{
  margin:0px;
}
i{
  cursor: pointer;
}
.bg el-button,.bg2 el-button{
  padding: 0px !important;
  margin: 0px !important;
}
.successAlert{
  color:green
}
</style>
