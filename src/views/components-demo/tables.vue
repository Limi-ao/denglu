<template>
  <div>
    <el-tabs type="border-card" style="height:100%">
      <el-tab-pane label="用户列表" style="margin-bottom:50px;">
        <el-table
          ref="multipleTable"
          :data="userList"
          style="cursor:pointer"
          border
          stripe
          tooltip-effect="dark"
          @selection-change="handleSelectionChange"
          @row-click="clickRowSelect"
        >
          <el-table-column
            type="selection"
            width="55"
            align="center"
          />
          <el-table-column
            prop="id"
            label="ID"
            width="200"
            align="center"
          />
          <el-table-column
            prop="name"
            label="姓名"
            width="200"
            align="center"
          />
          <el-table-column
            prop="sex"
            label="性别"
            width="200"
            align="center"
          />
          <el-table-column
            prop="age"
            label="年龄"
            width="200"
            align="center"
          />
          <el-table-column label="省份" width="200" align="center" prop="address" />
          <el-table-column
            prop="description"
            align="center"
            label="描述"
            show-overflow-tooltip
          />
          <el-table-column
            label="操作"
            width="200"
            align="center"
          >
            <template slot-scope="scope">
              <el-button type="primary" size="small" @click.stop="editRow(scope.$index,scope.row)">
                修改
              </el-button>
              <el-button
                type="danger"
                size="small"
                @click.stop="deleteRow(scope.$index, scope.row)"
              >
                移除
              </el-button>
            </template>
          </el-table-column>
        </el-table>
        <el-pagination
          style="padding-bottom:30px;position:fixed;bottom:0px;background:#ffffff"
          :current-page="currentPage"
          :page-sizes="[10, 50, 100]"
          :page-size="10"
          layout="total, sizes, prev, pager, next, jumper"
          :total="total"
          @size-change="handleSizeChange"
          @current-change="handleCurrentChange"
        />
      </el-tab-pane>
      <el-tab-pane label="设备列表"><img src="/img/back.png" alt=""></el-tab-pane>
      <el-tab-pane label="资源列表">角色管理</el-tab-pane>
      <el-tab-pane label="任务列表">定时任务补偿</el-tab-pane>
    </el-tabs>
    <el-dialog title="修改" :visible="showEditUser" :before-close="showEditUserInfo">
      <el-form ref="editUserForm" :model="editUserForm" :rules="rules" label-width="100px">
        <el-form-item label="姓名" prop="name" style="width:50%">
          <el-input v-model="editUserForm.name" />
        </el-form-item>
        <el-form-item label="性别" prop="sex">
          <el-radio-group v-model="editUserForm.sex">
            <el-radio label="男" />
            <el-radio label="女" />
          </el-radio-group>
        </el-form-item>
        <el-form-item label="年龄" prop="age" required>
          <el-input-number v-model="editUserForm.age" :min="1" :max="120" label="用户年龄" />
        </el-form-item>
        <el-form-item label="省份" prop="address">
          <el-input v-model="editUserForm.address" />
        </el-form-item>
        <el-form-item label="描述" prop="description">
          <el-input v-model="editUserForm.description" type="textarea" />
        </el-form-item>
        <el-form-item>
          <el-button type="primary" @click="submitForm('editUserForm')">修改</el-button>
          <el-button @click="showEditUserInfo">取消</el-button>
        </el-form-item>
      </el-form>
    </el-dialog>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'Tables',
  data() {
    return {
      $name: '123',
      userList: [],
      selectedRows: [],
      total: 0,
      editUserForm: {},
      showEditUser: false,
      currentPage: 1,
      size: 10,
      rules: {
        name: [
          { required: true, message: '姓名不能为空', trigger: 'blur' },
          { min: 2, max: 5, message: '长度在 2 到 5 个字符', trigger: 'blur' }
        ],
        sex: [
          { required: true, message: '性别不能为空', trigger: 'change' }
        ]
      }
    }
  },
  mounted() {
    this.getUserList()
  },
  methods: {
    getUserList() {
      axios.get('https://www.easy-mock.com/mock/5d1c63ad5a92b35a16acf307/mulTable', { params: { currentPage: this.currentPage, size: this.size }}).then(res => {
        this.userList = res.data.data
        this.total = res.data.total
      })
    },
    handleSelectionChange(row) {
      this.selectedRows = row
    },
    clickRowSelect(row) {
      this.$refs.multipleTable.toggleRowSelection(row)
    },
    handleSizeChange(size) {
      this.size = size
      this.getUserList()
    },
    handleCurrentChange(current) {
      this.current = current
      this.getUserList()
    },
    editRow(index, data) {
      this.showEditUser = true
      this.editUserForm = data
    },
    deleteRow(index, row) {
      this.$swal({
        title: '提示',
        type: 'warning',
        showCancelButton: true,
        cancelText: '取消',
        confirmButtonText: '确认删除'
      }).then(res => {
        if (res.value) {
          this.$swal({
            type: 'success',
            title: '删除成功'
          })
        }
      })
    },
    submitForm(formName) {
      this.$refs[formName].validate((valid) => {
        if (valid) {
          this.$swal({
            type: 'success',
            text: '修改成功'
          })
          this.showEditUser = false
          this.getUserList()
        } else {
          return false
        }
      })
    },
    showEditUserInfo() {
      this.showEditUser = false
    }
  }
}
</script>

<style scoped>

</style>
