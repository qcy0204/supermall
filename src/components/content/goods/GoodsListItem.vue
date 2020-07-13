<template>
  <div class="goods">
    <img :src="goods.show.img" alt="">
    <div  class="goods-info">
      <p>{{goods.title}}</p>
      <span class="price">{{goods.price}}</span>
      <span class="collect">{{goods.cfav}}</span>
    </div>
  </div>
</template>

<script>
export default {
  props:{
    goods:{
      type:Object,
      default(){
        return {}
      }
    }
  },
  data () {
    return {
    }
  },
  methods: {}
}
</script>

<style scoped>
.goods {
    padding-bottom: 2.6rem;
    position: relative;
    width: 45vw;
    height: 45vh;
  }
  .goods img {
    width: 100%;
    border-radius: 0.2rem;
  }

  .goods-info {
    font-size: 0.75rem;
    position: absolute;
    bottom: 0.2rem;
    left: 0;
    right: 0;
    overflow: hidden;
    text-align: center;
  }

  .goods-info p {
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
    margin-bottom: 0.1rem;
  }

  .goods-info .price {
    color: var(--color-high-text);
    margin-right: 1.2rem;
  }

  .goods-info .collect {
    position: relative;
  }

  .goods-info .collect::before {
    content: '';
    position: absolute;
    left: -15px;
    top: 0;
    width: 14px;
    height: 14px;
    background: url("~assets/img/common/collect.svg") 0 0/14px 14px;
  }
</style>
