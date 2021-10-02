<template>
  <div class="tab" @click="ItemClick">
    <div v-if="!isActive">
      <slot name="slot-img"></slot>
    </div>
    <div v-else>
      <slot name="slot-img-active"></slot>
    </div>
    <div :style="activeStyle">
      <slot name="slot-text"></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: "TabBarItem",
  data() {
    return {
      // isActive: true
    };
  },
  // created () {
  //   console.log(this.path);
  // },
  computed: {
    isActive(){
      // 判断当前的路由是否等于活跃的路由，是则返回true ，不是则返回false
      return this.$route.path.indexOf(this.path) !== -1
    },
    activeStyle(){
      // 如果isActive是true 则给其样式activeColor， 否则为空样式
      return this.isActive ? {color:this.activeColor} : {}
    }
  },
  props: {
    path: String,
    activeColor: {
      type: String,
      default: "red"
    }
  },
  methods: {
    ItemClick() {
      this.$router.replace(this.path).catch(error => error);
      console.log(this.$router);
    }
  }
};
</script>

<style>
.tab {
  flex: 1;
  text-align: center;
  height: 49px;
}

.tab img {
  vertical-align: middle;
  width: 24px;
  height: 24px;
  margin-bottom: 2px;
}

.active {
  color: red;
}
</style>
