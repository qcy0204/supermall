<template>
<!-- 返回顶部的封装 -->
  <div class="back-top">
   <img src="~assets/img/common/top.png" alt="">
  </div>
</template>

<script>
export default {
  data () {
    return {
    }
  }
}
</script>

<style scoped>
.back-top{
  position: fixed;
  right: 15px;
  bottom: 50px;
}
.back-top img{
  width: 43px;
  height: 43px;
}
</style>
