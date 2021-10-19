<template>
  <!-- 积分等级列表 -->
  <div class="app-container">
    <!-- 表格 -->
    <el-table :data="list" border stripe>
      <el-table-column type="index" width="50" />
      <el-table-column prop="borrowAmount" label="借款额度" />
      <el-table-column prop="integralStart" label="积分区间开始" />
      <el-table-column prop="integralEnd" label="积分区间结束" />
      <el-table-column label="操作">
        <template slot-scope="scope">
          <router-link :to="'/core/integral-grade/edit/' + scope.row.id">
            <el-button size="mini">编辑</el-button>
          </router-link>
          <el-button size="mini" type="danger" @click="removeById(scope.row.id)">删除</el-button>
        </template>

      </el-table-column>
    </el-table>
  </div>
</template>

<script>
import integralGradeApi from '@/api/core/integral-grade'

export default {
  data() {
    return {
      list: [],
    }
  },

  created() {
    this.fetchData()
  },

  methods: {
    fetchData() {
      integralGradeApi.list().then((response) => {
        this.list = response.data.list
      })
    },
    removeById(id) {
      this.$confirm('此操作将永久删除该记录, 是否继续?', '提示', {
        confirmButtonText: '确定',
        cancelButtonText: '取消',
        type: 'warning',
      }).then(() => {
        integralGradeApi
          .removeById(id)
          .then((response) => {
            this.$message({
              type: 'success',
              message: response.message,
            })
            this.fetchData()
          })
          .catch(() => {
            this.$message({
              type: 'info',
              message: '取消删除',
            })
          })
      })
    },
  },
}
</script>

<style>
</style>