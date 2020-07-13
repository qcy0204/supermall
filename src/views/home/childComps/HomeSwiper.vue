<template>
  <Swiper>
    <SwiperItem v-for="(item,index) in banners" :key="index">
      <a :href="item.link">
        <!--   @load="imageLoad" -->
        <img :src="item.image"/>
      </a>
    </SwiperItem>
  </Swiper>
</template>

<script>
// 轮播图
import {Swiper, SwiperItem} from "common/swiper/index";
export default {
  name: "HomeSwiper",
  props:{
    banners:{
      type:Array,
      default() {
        return []
      }
    }
  },
  components: {
    Swiper,
    SwiperItem
  },
  data() {
    return {
      isLoad:false
    };
  },
  methods: {
    // imageLoad(){
    //   // 避免反复获取四次
    //   if(!this.isLoad){
    //   this.$emit('swiperImageLoad')
    //   this.isLoad=true
    //   }
    // }
  }
};
</script>

<style scoped>
</style>
