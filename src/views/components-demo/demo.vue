<template>
  <div>
    <iframe :src="url" frameborder="0" width="100%" style="min-height:845px;" />
  </div>
</template>

<script>
export default {
  name: 'Demo',
  data() {
    return {
      url: '/pages/index.html'
    }
  }
  // watch: {
  //   $route(to, from) {
  //     this.$swal({
  //       title: '确定离开本页面吗，该页面无法缓存',
  //       type: 'warning',
  //       showCancelButton: true
  //     })
  //   }
  // }
  // beforeRouteLeave(to, from, next) {
  //   this.$confirm('本页面离开后需要重新加载，确定离开', '提示', {
  //     confirmButtonText: '确定',
  //     cancelButtonText: '取消',
  //     type: 'warning'
  //   }).then(() => {

  //   }).catch(() => {})
  // }
}
</script>

<style scoped>

</style>
