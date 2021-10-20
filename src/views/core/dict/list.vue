<template>
  <div class="app-container">
    <el-button type="primary" @click="dialogVisible = true">导入excel</el-button>
    <el-dialog title="提示" :visible.sync="dialogVisible" width="30%" :before-close="handleClose">
      <span>选择导入的excel文档</span>
      <el-upload class="upload-demo" :auto-upload="true" :action="BASE_API + '/admin/core/dict/import'" multiple :limit="1" :on-exceed="fileUploadExceed" :on-success="fileUploadSuccess" :on-error="fileUploadError" accept="application/vnd.ms-excel,application/vnd.openxmlformats-officedocument.spreadsheetml.sheet">
        <br>
        <el-button size="small" type="primary">点击上传</el-button>
        <!-- <div slot="tip" class="el-upload__tip">只能上传jpg/png文件，且不超过500kb</div> -->
      </el-upload>
      <span slot="footer" class="dialog-footer">
        <el-button @click="dialogVisible = false">取 消</el-button>
        <!-- <el-button type="primary" @click="dialogVisible = false">确 定</el-button> -->
      </span>
    </el-dialog>
    <br>
    <br>
    <el-button @click="exportData" type="primary" size="mini" icon="el-icon-upload2">导出Excel</el-button>
  </div>
</template>


<script>
export default {
  data() {
    return {
      dialogVisible: false,
      BASE_API: process.env.VUE_APP_BASE_API,
    }
  },

  methods: {
    fileUploadExceed() {
      this.$message.warning('只能选取一个文件')
    },
    fileUploadSuccess(response) {
      if (response.code === 0) {
        this.$message.success('数据导入成功')
        this.dialogVisible = false
      } else {
        this.$message.error(response.message)
      }
    },
    fileUploadError(error) {
      this.$message.error('数据导入失败')
    },
    exportData() {
      window.location.href = this.BASE_API + '/admin/core/dict/export'
    },
  },
}
</script>

<style>
</style>