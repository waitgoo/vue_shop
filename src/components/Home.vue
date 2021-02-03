<template>
  <div>
    <el-button type="info" @click="logout">退出</el-button>
  </div>
</template>

<script>
export default {
  methods: {
    logout() {
      window.sessionStorage.clear()
      this.$router.push('/login')
      // this.$message.warning('退出成功~')
      this.$message({
        message: '退出成功~',
        type: 'warning',
        center: true
      })
    }
  }
}
</script>

<style lang="less" scoped>

</style>
