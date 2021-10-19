<template>
  <div class="app-container">
    <!-- 积分等级表单 -->
    <el-form label-width="120px">
      <el-form-item label="借款额度">
        <el-input v-model="integralGrade.borrowAmount"></el-input>
      </el-form-item>
      <el-form-item label="积分区间开始">
        <el-input v-model="integralGrade.integralStart"></el-input>
      </el-form-item>
      <el-form-item label="积分区间结束">
        <el-input v-model="integralGrade.integralEnd"></el-input>
      </el-form-item>
      <el-button :disabled="saveBtnDisabled" type="primary" @click="saveOrUpdate()">保存</el-button>
      <!-- <el-button>取消</el-button> -->
    </el-form>
  </div>
</template>
<script>
import integralGradeApi from '@/api/core/integral-grade'

export default {
  data() {
    return {
      integralGrade: {},
      saveBtnDisabled: false,
    }
  },
  created() {
    if (this.$route.params.id) {
      this.fetchDataById(this.$route.params.id)
    }
  },
  methods: {
    //新增
    saveOrUpdate() {
      this.saveBtnDisabled = true
      if (this.integralGrade.id) {
        this.updateData()
      } else {
        this.saveData()
      }
    },
    saveData() {
      integralGradeApi
        .save(this.integralGrade)
        .then((response) => {
          this.$message({
            type: 'success',
            message: response.message,
          })
          this.$router.push('/core/integral-grade/list')
        })
        .catch(() => {
          this.saveBtnDisabled = false
        })
    },
    //修改
    fetchDataById(id) {
      integralGradeApi.getById(id).then((response) => {
        this.integralGrade = response.data.record
      })
    },
    updateData() {
      integralGradeApi
        .updateById(this.integralGrade)
        .then((response) => {
          this.$message({
            type: 'success',
            message: response.message,
          })
          this.$router.push('/core/integral-grade/list')
        })
        .catch(() => {
          this.saveBtnDisabled = false
        })
    },
  },
}
</script>

<style >
</style>