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
  methods: {
    sleep(time) {
      return new Promise((resolve) => setTimeout(resolve, time))
    },
    saveOrUpdate() {
      this.saveBtnDisabled = true
      this.saveData()
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
  },
}
</script>

<style >
</style>