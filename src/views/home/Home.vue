<template>
  <div id="home">
    <!-- 导航 -->
    <nav-bar class="home-nav">
      <div slot="center">购物街</div>
    </nav-bar>
    <!-- 滚动 -->
    <scroll class="content" ref="scroll" :probe-type="3" :pull-up-load="true" @scroll="contentscroll" @pullingUp="loadMore">
      <!-- 轮播图   @swiperImageLoad="swiperImageLoad"-->
      <home-swiper :banners="banners"></home-swiper>
      <!-- 推荐信息 -->
      <home-recommend-view :recommends="recommends"></home-recommend-view>
      <!-- 本周流行 -->
      <home-Feature-view></home-Feature-view>
      <!-- 内容 -->
      <tab-control
        class="tab-control"
        ref="tabControl"
        :title="['流行','新款','精选']"
        @tabClick="tabClick"
      ></tab-control>
      <goods-list :goods="goods[currenType].list"></goods-list>
    </scroll>
    <!-- 监听组件点击 必须加native -->
    <back-top @click.native="backClick" v-show="isShowBackTop"></back-top>
  </div>
</template>

<script>
// ----公共的
// 导航
import NavBar from "common/navbar/NavBar";
import TabControl from "content/tabControl/TabControl";
import GoodsList from "content/goods/GoodsList";
import Scroll from "common/scroll/Scroll";
import BackTop from "content/BackTop";
// ----子组件
// 轮播图
import HomeSwiper from "./childComps/HomeSwiper";
// 推荐信息
import HomeRecommendView from "./childComps/HomeRecommendView";
// 本周流行
import HomeFeatureView from "./childComps/HomeFeatureView";

// ---数据请求
// home请求
import { getHomeMultidata, getHomeGoods } from "network/home";
export default {
  name: "home",
  components: {
    NavBar,
    HomeSwiper,
    HomeRecommendView,
    HomeFeatureView,
    TabControl,
    GoodsList,
    Scroll,
    BackTop
  },
  data() {
    return {
      // 1.轮播图
      banners: [],
      // 2.推荐信息
      recommends: [],
      // 3.内容  流行~~~
      goods: {
        pop: { page: 0, list: [] },
        new: { page: 0, list: [] },
        sell: { page: 0, list: [] }
      },
      currenType: "pop",
      isShowBackTop: false
      // 固定流行 新款  精选的位置
      // tabOffsetTop:0
    };
  },
  created() {
    // 1.首页数据
    getHomeMultidata().then(res => {
      // console.log(res.data);
      this.banners = res.data.banner.list;
      this.recommends = res.data.recommend.list;
    });
    this.getHomeGoods("pop");
    this.getHomeGoods("new");
    this.getHomeGoods("sell");
  },
  methods: {
    // 网络请求
    getHomeGoods(type) {
      const page = this.goods[type].page + 1;
      // 2.内容goods数据
      getHomeGoods(type, page).then(res => {
        //  console.log(res.data);
        this.goods[type].list.push(...res.data.list);
        this.goods[type].page += 1;

        this.$refs.scroll.finishPullUp()
      });
    },

    // 事件监听
    // 1.流行 新款  精选的切换
    tabClick(index) {
      // console.log(index)
      if (index == 0) {
        this.currenType = "pop";
      } else if (index == 1) {
        this.currenType = "new";
      } else {
        this.currenType = "sell";
      }
    },
    // 2
    backClick() {
      // console.log('1')
      // 点击 回到顶部
      this.$refs.scroll.scrollTo(0, 0, 500);
    },
    // 2.1
    contentscroll(position) {
      // console.log(position)
      // 判断到某个位置的显示和隐藏
      this.isShowBackTop = -position.y > 1000;
    },
    // 3 上拉加载更多
    loadMore(){
      this.getHomeGoods(this.currenType)
      this.$refs.scroll.scroll.refresh()
    }
    // ,
    // // 流行 新款  精选的固定
    // swiperImageLoad(){
    //   // 屏幕尺寸
    //   // console.log(this.$refs.tabControl.$el.offsetTop)
    //   this.tabOffsetTop=this.$refs.tabControl.$el.offsetTop
    // }
  }
};
</script>

<style scoped>
#home {
  padding-top: 44px;
  height: 100vh;
  position: relative;
}
.home-nav {
  background-color: var(--color-tint);
  color: #fff;
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 9;
}
/* 定位吸顶  老游览器不行 */
.tab-control {
  /* position: sticky;
  top: 44px; */
}
.content {
  overflow: hidden;
  position: absolute;
  top: 44px;
  bottom: 49px;
  left: 0;
  right: 0;
}
</style>
