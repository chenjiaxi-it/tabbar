<template>
  <div class="wrapper" ref="wrapper">
    <div class="content">
      <slot></slot>
    </div>
  </div>
</template>

<script>
import BScroll from "better-scroll";
export default {
  name: "Scroll",
  props: {
    probeType: {
      type: Number,
      default: 0,
    },
    pullUpLoad: {
      type: Boolean,
      default: false,
    },
  },
  data() {
    return {
      scroll: null,
    };
  },
  mounted() {
    //1.创建BScroll对象
    this.scroll = new BScroll(this.$refs.wrapper, {
      click: true,
      probeType: this.probeType, //实时监听上拉位置
      pullUpLoad: this.pullUpLoad, //上拉加载事件，默认不需要
    });
    //2.监听滚动位置
    this.scroll.on("scroll", (position) => {
      // console.log(position);
      this.$emit("scroll", position);
    });
    //3.监听上拉刷新事件
    this.scroll.on("pullingUp", () => {
      this.$emit("pullingup");
      // console.log("上拉加载更多");
    });
  },
};
</script>
<style scoped>
</style>
