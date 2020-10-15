<template>
  <div class="index content">
    <div class="top">
      <div class="left">
        <div class="left-item left-top">
          <div class="item-title">
            <img src="./play.png" alt="" class="left-img" />
            <div class="mL10">小程序注册用户数</div>
          </div>
          <div class="top-border">
            <count-to :end="20399" count-class="count-style" class="item-num" />
            <div>2020年7月29日</div>
          </div>
        </div>
        <div class="left-item left-bottom">
          <div class="item-title">
            <img src="./play.png" alt="" class="left-img" />
            <div class="mL10">小程序总访问量</div>
          </div>
          <div class="top-border">
            <count-to :end="20399" count-class="count-style" class="item-num" />
            <div>2020年7月29日</div>
          </div>
        </div>
      </div>

      <div class="map">
        <div class="map-title">地图</div>
        <div id="mapContainer"></div>

        <!-- <div ref="chart2" style="width:100%;height:100%"></div> -->
      </div>
      <div class="right">
        <div class="map-title">性别统计</div>
        <div>
          <div ref="chart2" class="chart2"></div>
        </div>
      </div>
    </div>

    <div class="bottom">
      表格
      <div ref="chart1" style="width: 100%; height: 100%"></div>
    </div>

    <div class="top" style="margin-top:20px">
      <div class="left" >
        <div class="left-item left-top">
          <div class="item-title">
            <img src="./play.png" alt="" class="left-img" />
            <div class="mL10">小程序注册用户数</div>
          </div>
          <div class="top-border">
            <count-to :end="20399" count-class="count-style" class="item-num" />
            <div>2020年7月29日</div>
          </div>
        </div>
        <div class="left-item left-bottom">
          <div class="item-title">
            <img src="./play.png" alt="" class="left-img" />
            <div class="mL10">小程序总访问量</div>
          </div>
          <div class="top-border">
            <count-to :end="20399" count-class="count-style" class="item-num" />
            <div>2020年7月29日</div>
          </div>
        </div>
      </div>

      <div class="bottom2" >
        <div ref="chart1" style="width: 100%; height: 100%"></div>
      </div>
      <!-- <div class="map">
        <div class="map-title">地图</div>
        <div id="mapContainer"></div>

      </div>
      <div class="right">
        <div class="map-title">性别统计</div>
        <div>
          <div ref="chart2" class="chart2"></div>
        </div>
      </div> -->
    </div>

    <div class="bottom">
      词条云
      <div id="my_canvas" style="width: 100%; height: 90%"></div>
    </div>

    <div class="" style="margin-top: 30px">
      <Row :gutter="32" style="margin-top: 20px">
        <Col span="8">
          <div class="item">
            <div class="left-item">
              <div class="item-title">
                <img src="./play.png" alt="" class="left-img" />
                <div class="mL10">政策数</div>
              </div>
              <div class="top-border">
                <count-to
                  :end="20399"
                  count-class="count-style"
                  class="item-num"
                />
                <div>2020年7月29日</div>
              </div>
            </div>
          </div>
        </Col>
        <Col span="8">
          <div class="item">
            <div class="left-item">
              <div class="item-title">
                <img src="./play.png" alt="" class="left-img" />
                <div class="mL10">标准数</div>
              </div>
              <div class="top-border">
                <count-to
                  :end="20399"
                  count-class="count-style"
                  class="item-num"
                />
                <div>2020年7月29日</div>
              </div>
            </div>
          </div>
        </Col>
        <Col span="8">
          <div class="item">
            <div class="left-item">
              <div class="item-title">
                <img src="./play.png" alt="" class="left-img" />
                <div class="mL10">机构动态数</div>
              </div>
              <div class="top-border">
                <count-to
                  :end="20399"
                  count-class="count-style"
                  class="item-num"
                />
                <div>2020年7月29日</div>
              </div>
            </div>
          </div>
        </Col>
      </Row>
    </div>

    <div class="">
      <Row :gutter="32" style="margin-top: 20px">
        <Col span="8">
          <div class="item">
            <div class="left-item">
              <div class="item-title">
                <img src="./play.png" alt="" class="left-img" />
                <div class="mL10">资讯数</div>
              </div>
              <div class="top-border">
                <count-to
                  :end="20399"
                  count-class="count-style"
                  class="item-num"
                />
                <div>2020年7月29日</div>
              </div>
            </div>
          </div>
        </Col>
        <Col span="8">
          <div class="item">
            <div class="left-item">
              <div class="item-title">
                <img src="./play.png" alt="" class="left-img" />
                <div class="mL10">入职机构数</div>
              </div>
              <div class="top-border">
                <count-to
                  :end="20399"
                  count-class="count-style"
                  class="item-num"
                />
                <div>2020年7月29日</div>
              </div>
            </div>
          </div>
        </Col>
        <Col span="8">
          <div class="item">
            <div class="left-item">
              <div class="item-title">
                <img src="./play.png" alt="" class="left-img" />
                <div class="mL10">公益服务数</div>
              </div>
              <div class="top-border">
                <count-to
                  :end="20399"
                  count-class="count-style"
                  class="item-num"
                />
                <div>2020年7月29日</div>
              </div>
            </div>
          </div>
        </Col>
      </Row>
    </div>

    <div class="bottom">
      表格
      <div ref="chart1" style="width: 100%; height: 100%"></div>
    </div>
  </div>
</template>

<script>
import echarts from "echarts";
import CountTo from "_c/count-to";
// import WordCloud from 'wordcloud'
import js2wordcloud from "js2wordcloud";
export default {
  data() {
    return {
      option1: {
        xAxis: {
          type: "category",
          data: ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"],
        },
        yAxis: {
          type: "value",
        },
        series: [
          {
            data: [820, 932, 901, 934, 1290, 1330, 1320],
            type: "line",
          },
        ],
      },

      option2: {
        legend: {
          // orient: "vertical",
          left: 10,
          top: window.screen.width < 1400 ? 240 : 300,
          data: ["直接访问", "邮件营销"],
        },
        tooltip: {
          trigger: "item",
          formatter: "{a} <br/>{b}: {c} ({d}%)",
        },

        series: [
          {
            name: "访问来源",
            type: "pie",
            radius: ["50%", "70%"],
            avoidLabelOverlap: false,
            label: {
              show: false,
              position: "center",
            },
            emphasis: {
              label: {
                show: true,
                fontSize: "30",
                fontWeight: "bold",
              },
            },
            labelLine: {
              show: false,
            },
            data: [
              { value: 335, name: "直接访问" },
              { value: 310, name: "邮件营销" },
              { value: 234, name: "联盟广告" },
              { value: 135, name: "视频广告" },
              { value: 1548, name: "搜索引擎" },
            ],
          },
        ],
      },
    };
  },
  components: {
    CountTo,
  },
  computed: {},
  mounted() {
    var wc = new js2wordcloud(document.getElementById("my_canvas"));

    wc.setOption({
      list: [
        ["foo", 80],
        ["bar", 80],
        ["foo", 80],
        ["bar", 60],
        ["foo", 30],
        ["bar", 60],
        ["foo", 80],
        ["bar", 60],
        ["foo", 32],
        ["bar", 60],
      ],
      scale: 1,
      color: "random-dark",
      // shape: 'circle',
      ellipticity: 1,
      minRotation: -1.5708,
      maxRotation: -1.5708,
      rotateRatio: 0.4,
      fontSizeFactor: 5, // 当词云值相差太大，可设置此值进字体行大小微调，默认0.1
      maxFontSize: 60, // 最大fontSize，用来控制weightFactor，默认60
      minFontSize: 20,
      gridSize: 10,
      // ratationSteps: 2,
      // rotationRation: .5,
      // shuffle: 30
      // shape: 'circle',
      // cardioid: 'diamond'
      cardioid: "square",
    });
    window.onresize = function () {
      wc.resize();
    };

    let myChart1 = echarts.init(this.$refs.chart1);
    myChart1.setOption(this.option1, true);

    let myChart2 = echarts.init(this.$refs.chart2);
    myChart2.setOption(this.option2, true);

    var center = new TMap.LatLng(39.984104, 116.307503);
    // 初始化地图
    var map = new TMap.Map("mapContainer", {
      zoom: 8, // 设置地图缩放级别
      center: center, // 设置地图中心点坐标
      disableDefaultUI: true,
      zoomControl: false,
      // mapStyleId: "style1", //个性化样式
      // disableDoubleClickZoom: false
    });
    // 创建散点图
    var dot = new TMap.visualization.Dot({
      faceTo: "screen", // 设置散点朝向
      styles: {
        redCircle: {
          // 定义一个红色圆形样式
          type: "circle",
          fillColor: "#FF0000",
        },
      },
    }).addTo(map);
    dot.setData([
      { lat: 40.040934, lng: 116.272677, styleId: "redCircle" },
      { lat: 40.04035, lng: 116.262432, styleId: "redCircle" },
    ]);

    setTimeout(() => {
      var con = document.getElementById("mapContainer");
      con.lastChild.style.display = "none";
    }, 0);
  },
};
</script>

<style scoped lang="less">
@import "~@/assets/variables.less";
// .content{
//   text-align: center;
// }
.top {
  width: 1312px;
  height: 510px;
  background: #ffffff;

  margin: 0 auto;
}
.bottom {
  width: 1312px;
  height: 370px;
  background: #ffffff;
  border-radius: 10px;
  box-shadow: 0px 2px 14px 0px rgba(0, 0, 0, 0.11);
  margin: 0 auto;
  margin-top: 20px;
}

.bottom2 {
  width: 900px;
  height: 471px;
  background: #ffffff;
  border-radius: 10px;
  box-shadow: 0px 2px 14px 0px rgba(0, 0, 0, 0.11);
vertical-align:top;
  display: inline-block;
}

.left {
  width: 360px;
  height: 471px;
  margin-right: 20px;
  display: inline-block;
  border-radius: 10px;
  box-shadow: 0px 2px 14px 0px rgba(0, 0, 0, 0.11);
}

.left-item {
  padding-left: 10px;
  width: 360px;
  height: 231px;
  background: #000;
  color: @Cffffff;
  border-radius: 10px;
}
.left-img {
  width: 50px;
  height: 50px;
}
.left-top {
}
.left-bottom {
  margin-top: 5px;
}
.item-title {
  // margin-top: 10px;
  margin-bottom: 30px;
  padding-top: 15px;
  // padding-bottom: 10px;
  height: 50px;
  line-height: 50px;
  width: 100%;
  // border-bottom: 1px solid #1c1c1c;
  vertical-align: top;
  display: flex;
}
.top-border {
  border-top: 1px solid #1c1c1c;
}

.item-num {
  // padding-top: 10px;
  font-size: 28px;
  text-align: left;
}

.map {
  width: 550px;
  height: 471px;
  margin-right: 20px;
  display: inline-block;
  vertical-align: top;
  border-radius: 10px;
  overflow: hidden;
  box-shadow: 0px 2px 14px 0px rgba(0, 0, 0, 0.11);
}
#mapContainer {
  height: 100%;
}
.map-title {
  padding: 10px;
  font-size: 19px;
  font-family: Celias-Medium;
  text-align: left;
  color: #566770;
}
.right {
  width: 340px;
  height: 471px;
  display: inline-block;
  vertical-align: top;
  border-radius: 10px;
  box-shadow: 0px 2px 14px 0px rgba(0, 0, 0, 0.11);
}

.item {
  padding-left: 20px;
  width: 100%;
  height: 231px;
}
.chart2 {
  margin-top: -30px;
  width: 100%;
  height: 400px;
}
@media (max-width: 1400px) {
  .top {
    width: calc(~"var(--ratio) * 1312px");
    height: calc(~"var(--ratio) * 510px");
  }
  .bottom {
    width: calc(~"var(--ratio) * 1312px");
    height: calc(~"var(--ratio) * 370px");
  }

  .bottom2 {
    width: calc(~"var(--ratio) * 900px");
    height: calc(~"var(--ratio) * 471px");
  }

  .left {
    width: calc(~"var(--ratio) * 360px");
    height: calc(~"var(--ratio) * 471px");
  }
  .left-item {
    width: calc(~"var(--ratio) * 360px");
    height: calc(~"var(--ratio) * 231px");
  }
  .item-title {
    height: calc(~"var(--ratio) * 50px");
    line-height: calc(~"var(--ratio) * 50px");
  }
  .map {
    width: calc(~"var(--ratio) * 550px");
    height: calc(~"var(--ratio) * 471px");
  }
  .right {
    width: calc(~"var(--ratio) * 340px");
    height: calc(~"var(--ratio) * 471px");
  }
  .item {
    // height: calc(~"var(--ratio) * 160px");
    height: calc(~"var(--ratio) * 231px");
  }
  .left-img {
    width: calc(~"var(--ratio) * 50px");
    height: calc(~"var(--ratio) * 50px");
  }
  .chart2 {
    height: calc(~"var(--ratio) * 400px");
  }
}
</style>
