<template>
  <div>
    <div :id="radarChart"
         style="width:350px;height:280px"></div>
  </div>
</template>
<script>
import * as echarts from 'echarts'
const idGen = () => {
  return new Date().getTime()
}
export default {
  props: {
    options: {
      type: Object,
      default: null
    },
    color: {
      type: String,
      default: 'rgb(155, 191, 253)'
    },
  },
  name: 'RadarChart',
  data () {
    return {
      radarChart: null
    }
  },
  mounted () {
    setTimeout(() => {
      this.renderEcharts();
    }, 500);
  },
  created () {
    this.radarChart = idGen()
  },
  watch: {
    options: {
      immediate: true,
      deep: true,
      handler (val) {
        this.options = val;
        // let _this = this
        // _this.renderEcharts();
        setTimeout(() => {
          // debugger
          this.renderEcharts();
        }, 500);
      }
    },
    // options (val) {
    //   this.options = val;
    //   setTimeout(() => {
    //     this.renderEcharts();
    //   }, 500);
    // },
  },
  methods: {
    renderEcharts () {
      var roseCharts = document.getElementById(this.radarChart);
      var myChart = echarts.init(roseCharts);
      var xDataArr = [];
      // debugger
      this.xDataArr.forEach((value, index) => {
        xDataArr.push({ name: value, max: 100 })
      });
      let option = {
        radar: {
          indicator: xDataArr,
          name: {
            textStyle: {
              fontSize: 15,
              color: '#333333'
            }
          },

        },
        series: [
          {
            //这里的配置显示数值
            label: {
              normal: {
                show: true,
                textStyle: {
                  color: this.color //雷达图数值颜色
                },
                formatter: function (params) {
                  return params.value;
                }
              },

            },
            type: 'radar',
            areaStyle: {

              normal: {
                color: this.color //改变区域颜色
              }
            },//背景色显示
            itemStyle: {
              normal: {
                color: this.color, //改变折线点的颜色
                lineStyle: {
                  color: this.color //改变折线颜色
                }
              }
            },
            data: [
              {
                // value: [70, 60, 100, 55, 75],
                value: this.options.yDataArr,
              }
            ]
          }
        ]
      };
      myChart.setOption(option);

    },
  }
}
</script>

<style scoped>
</style>
