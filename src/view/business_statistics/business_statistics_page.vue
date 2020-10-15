<template>
  <div class="index content">
    <div class="top">
      内容建设
    </div>
    <div class="outter">
      <Row :gutter="32" style="margin-top:20px;">
        <Col span="8">
          <div class="item">
            <div class="item-top">
              政策数
            </div>
            <count-to :end="20399" count-class="count-style" class="item-num" />
          </div>
        </Col>
        <Col span="8">
          <div class="item">
            <div class="item-top">
              资讯数
            </div>
            <count-to :end="20399" count-class="count-style" class="item-num" />
          </div>
        </Col>
        <Col span="8">
          <div class="item">
            <div class="item-top">
              标准数
            </div>
            <count-to :end="20399" count-class="count-style" class="item-num" />
          </div>
        </Col>
      </Row>
      <Row :gutter="32" style="margin-top:20px;">
        <Col span="8">
          <div class="item">
            <div class="item-top">
              机构动态数
            </div>
            <count-to :end="20399" count-class="count-style" class="item-num" />
          </div>
        </Col>
        <Col span="8">
          <div class="item">
            <div class="item-top">
              公益服务数
            </div>
            <count-to :end="20399" count-class="count-style" class="item-num" />
          </div>
        </Col>
        <Col span="8">
          <div class="item">
            <div class="item-top">
              问卷调查数
            </div>
            <count-to :end="20399" count-class="count-style" class="item-num" />
          </div>
        </Col>
      </Row>

      <Row :gutter="32" style="margin-top:20px;">
        <Col span="8">
          <div class="item long">
            <div class="item-top">
              政策数
            </div>
            <div class="chart-box">
              <div ref="chart1" style="width:100%;height:100%"></div>
            </div>

            <!-- <count-to :end="20399" count-class="count-style" class="item-num" /> -->
          </div>
        </Col>
        <Col span="8">
          <div class="item long">
            <div class="item-top">
              政策数
            </div>
            <count-to :end="20399" count-class="count-style" class="item-num" />
          </div>
        </Col>
        <Col span="8">
          <div class="item long">
            <div class="item-top">
              政策数
            </div>
            <count-to :end="20399" count-class="count-style" class="item-num" />
          </div>
        </Col>
      </Row>
    </div>

    <div class="top">
      民政方面
    </div>

    <div class="outter">
      <Row :gutter="32" style="margin-top:20px;">
        <Col span="8">
          <div class="item">
            <div class="item-top">
              完成机构认证数
            </div>
            <count-to :end="20399" count-class="count-style" class="item-num" />
          </div>
        </Col>
        <Col span="8">
          <div class="item">
            <div class="item-top">
              待审核认证数
            </div>
            <count-to :end="20399" count-class="count-style" class="item-num" />
          </div>
        </Col>
        <Col span="8">
          <div class="item">
            <div class="item-top">
              驳回机构认证数
            </div>
            <count-to :end="20399" count-class="count-style" class="item-num" />
          </div>
        </Col>
      </Row>
    </div>
  </div>
</template>

<script>
import echarts from 'echarts'
import CountTo from '_c/count-to'

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
    var dataAxis = [
      '点点',
      '击点',
      '柱点',
      '子点',
      '或点',
      '者点',
      '两点',
      '指点',
      '在点',
      '触点'
    ]
    var data = [220, 182, 191, 234, 290, 330, 310, 123, 442, 321]

    var option1 = {
      tooltip: {
        trigger: 'axis',
        formatter (params) {
          for (var x in params) {
            return params[x].name + ':' + params[x].data
          }
        }
      },
      xAxis: {
        data: dataAxis,
        axisLabel: {
          textStyle: {
            fontSize: 8
          },
          formatter: function (value) {
            // x轴的文字改为竖版显示
            var str = value.split('')
            return str.join('\n')
          }
        },
        axisTick: {
          length: 0
        },
        axisLine: {
          show: false
        },
        z: 0
      },
      yAxis: {
        show: false,
        axisLine: {},
        axisTick: {},
        axisLabel: {
          textStyle: {
            color: '#999'
          }
        }
      },

      series: [
        {
          type: 'bar',
          itemStyle: {
            normal: {
              color: function (params) {
                var colorList = [
                  '#E5E5E5',
                  '#CCCCCC',
                  '#B2B2B2',
                  '#999999',
                  '#7F7F7F',
                  '#666666',
                  '#4C4C4C',
                  '#333333',
                  '#191919',
                  '#000000'
                ]
                return colorList[params.dataIndex]
              }
            }
          },

          data: data
        }
      ]
    }

    let myChart1 = echarts.init(this.$refs.chart1)
    myChart1.setOption(option1, true)
    setTimeout(() => {
      myChart1.resize()
    }, 0)

    // window.addEventListener("resize", () => {
    //   myChart1.resize();
    // });
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
.top {
  font-size: 20px;
  margin-top: 20px;
  margin-left: 20px;
  // font-family: Helvetica Neue, Helvetica Neue-Bold;
  font-weight: 700;
  // text-align: center;
  color: #000000;
}
.item {
  // background: red;
  padding-left: 20px;
  width: 100%;
  height: 160px;
  border-radius: 10px;
  box-shadow: 0px 2px 14px 0px rgba(0, 0, 0, 0.11);

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
