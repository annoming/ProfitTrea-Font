<template>
  <div>
    <el-tabs class="panel" v-model="activeName" @tab-click="handleClick">
      <el-tab-pane label="组织列表" name="first">
        <span class="username-label">组织名称：</span>
        <el-input v-model="username" class="username-input"></el-input>
        <span class="date-label">创建时间：</span>
        <el-date-picker v-model="value2" type="datetimerange" :picker-options="pickerOptions" range-separator="To"
          start-placeholder="Start date" end-placeholder="End date" align="right">
        </el-date-picker>
        <br />
        <el-button class="btn" icon="el-icon-download">导出列表数据</el-button>
        <el-button class="btn" type="primary" icon="el-icon-plus" @click="addOrganize">新增组织</el-button>
        <el-button class="btn" type="primary" icon="el-icon-search">查询</el-button>
        <el-button class="btn" icon="el-icon-refresh-left">重置</el-button>
        <el-table ref="singleTable" :data="tableData" highlight-current-row style="width: 100%">
          <el-table-column type="index" width="120" label="序号">
          </el-table-column>
          <el-table-column property="date" label="日期" width="120">
          </el-table-column>
          <el-table-column property="name" label="用户名" width="120">
          </el-table-column>
          <el-table-column property="operate" label="操作">
          </el-table-column>
        </el-table>
      </el-tab-pane>
      <el-tab-pane label="待审核" name="second">待审核</el-tab-pane>
      <el-tab-pane label="审核不通过" name="third">审核不通过</el-tab-pane>
    </el-tabs>
    <AddOrganizeForm ref="setDialogVisible"></AddOrganizeForm>
  </div>
</template>

<script>
  import AddOrganizeForm from '@/components/administrator/AddOrganizeForm.vue'
  export default {
    name: 'panel',
    data() {
      return {
        activeName: 'first',
        username: '',
        pickerOptions: {
          shortcuts: [{
              text: 'Last week',
              onClick(picker) {
                const end = new Date()
                const start = new Date()
                start.setTime(start.getTime() - 3600 * 1000 * 24 * 7)
                picker.$emit('pick', [start, end])
              }
            },
            {
              text: 'Last month',
              onClick(picker) {
                const end = new Date()
                const start = new Date()
                start.setTime(start.getTime() - 3600 * 1000 * 24 * 30)
                picker.$emit('pick', [start, end])
              }
            },
            {
              text: 'Last 3 months',
              onClick(picker) {
                const end = new Date()
                const start = new Date()
                start.setTime(start.getTime() - 3600 * 1000 * 24 * 90)
                picker.$emit('pick', [start, end])
              }
            }
          ]
        },
        value1: [new Date(2000, 10, 10, 10, 10), new Date(2000, 10, 11, 10, 10)],
        value2: '',
        tableData: [
          /* {
            date: '',
            name: '',
            operate: ''
          } */
        ]
      }
    },
    methods: {
      handleClick(tab, event) {
        console.log(tab, event)
      },
      addOrganize () {
        this.$refs.setDialogVisible.init(true)
      }
    },
    components: {
      AddOrganizeForm
    }
  }
</script>

<style>
  .panel {
    width: 100%;
    margin-right: 200px;
  }

  .username-input {
    margin-right: 50px;
    width: 30%;
  }

  .btn {
    margin: 30px 20px 0 0;
  }

  .el-table {
    margin-top: 30px;
  }
</style>
