<template>
  <div class="recommends">
    <div v-for="(item,index) in recommends" :key="index" class="recommends-item">
      <a :href="item.link">
        <img :src="item.image" alt="" class="recommends-image">
        <div>{{item.title}}</div>
      </a>
    </div>
  </div>
</template>

<script>
export default {
  props:{
    recommends:{
      type:Array,
      default(){
        return []
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
.recommends{
  display: flex;
  width: 100%;
  text-align: center;
  border-bottom: 8px solid #eee;
}
.recommends-item{
  flex:1;
  padding:5px 10px 20px;
}
.recommends-item img{
  width: 100%;
}
</style>
