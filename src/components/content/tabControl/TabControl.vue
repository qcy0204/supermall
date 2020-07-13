<template>
  <div class="tab-control">
    <div
      v-for="(item,index) in title"
      :key="index"
      class="tab-item"
      :class="{active:index===currentIndex}"
      @click="itemCilck(index)"
    >
      <span>{{item}}</span>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    title: {
      type: Array,
      default() {
        return [];
      }
    }
  },
  data() {
    return {
      currentIndex: 0
    };
  },
  methods: {
    itemCilck(index) {
      this.currentIndex = index;
      this.$emit('tabClick',index)
    }
  }
};
</script>

<style scoped>
.tab-control {
  display: flex;
  text-align: center;
  font-size: 15px;
  height: 40px;
  line-height: 40px;
  background: #fff;
  z-index: 9;
}
.tab-item {
  flex: 1;
}
.tab-item span {
  padding: 10px;
}
.active {
  color: var(--color-high-text);
}
.active span {
  border-bottom: 3px solid var(--color-high-text);
}
</style>
