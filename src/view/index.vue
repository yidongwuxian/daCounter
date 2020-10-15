<template>
  <div class="index content">

    <div style="width:500px;height:500px">
      1
      <canvas id="my_canvas" style="width:500px;height:500px"></canvas>
    </div>
      <!-- <canvas id="my_canvas"></canvas> -->
  </div>
</template>

<script>
// import echarts from 'echarts'
import CountTo from '_c/count-to'
// import WordCloud from 'wordcloud'
export default {
  data () {
    return {}
  },
  components: {
    CountTo
    // customBreadCrumb
  },
  computed: {},
  mounted () {
    // WordCloud(document.getElementById('my_canvas'), { list: [['foo', 12], ['bar', 6], ['foo', 12], ['bar', 6], ['foo', 12], ['bar', 6], ['foo', 12], ['bar', 6], ['foo', 12], ['bar', 6]] })
  }
}
</script>

<style scoped lang="less">
@import "~@/assets/variables.less";
// .content{
//   text-align: center;
// }
.outter {
  margin-left: 10px;
}
.item {
  // background: red;
  padding-left: 20px;
  width: 100%;
  height: 160px;
  border-radius: 10px;
  box-shadow: 0px 2px 14px 0px rgba(0, 0, 0, 0.11);

  height: calc(~"var(--ratio) * 665px");
}
.long {
  height: 320px;
}
.chart-box {
  height: 270px;
}
.item-top {
  height: 50px;
  line-height: 50px;
}
.item-num {
  font-size: 28px;
  text-align: left;
}

@media (max-width: 1400px) {
  .item {
    height: calc(~"var(--ratio) * 160px");
  }
  .long {
    height: calc(~"var(--ratio) * 320px");
  }
  .chart-box {
    height: calc(~"var(--ratio) * 270px");
  }
}
</style>
