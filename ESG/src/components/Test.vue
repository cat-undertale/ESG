<template>

  <div>
    <div :id="radarChart" style="width: 350px; height: 280px"></div>
    <div>
      <VueTable></VueTable>
    </div>
  </div>

</template>
<script>
import * as echarts from "echarts";
import Home from "./Home";
import VueTable from "./VueTable";
const idGen = () => {
  return new Date().getTime();
};
export default {
  props: {
    // options: {
    //   type: Object,
    //   default: null
    // },
    color: {
      type: String,
      default: "rgb(155, 191, 253)",
    },
  },
  name: "RadarChart",
  components: {VueTable},
  data() {
    return {
      radarChart: null,
      xDataArr: [],
      yDataArr: [30, 40, 50],
    };
  },
  mounted() {
    setTimeout(() => {
      this.renderEcharts();
    }, 500);
  },
  created() {
    this.radarChart = idGen();
  },
  watch: {
    // options: {
    //   immediate: true,
    //   deep: true,
    //   handler(val) {
    //     this.options = val;
    //     // let _this = this
    //     // _this.renderEcharts();
    //     setTimeout(() => {
    //       // debugger
    //       this.renderEcharts();
    //     }, 500);
    //   },
    // },
    // options (val) {
    //   this.options = val;
    //   setTimeout(() => {
    //     this.renderEcharts();
    //   }, 500);
    // },
  },
  methods: {
    renderEcharts() {
      var roseCharts = document.getElementById(this.radarChart);
      var myChart = echarts.init(roseCharts);
      var xDataArr = [
        { name: "E", max: 100 },
        { name: "S", max: 100 },
        { name: "G", max: 100 },
      ];
      // debugger
      //   this.xDataArr.forEach((value, index) => {
      //     xDataArr.push({ name: value, max: 50 });
      //   });
      //    this.options.xDataArr.push({ name: "技术", max: 100 });
      //    this.options.xDataArr.push({ name: "商务", max: 100 });
      //    this.options.xDataArr.push({ name: "能力", max: 100 });

      var option = {
        radar: {
          indicator: xDataArr,
          name: {
            textStyle: {
              fontSize: 15,
              color: "#333333",
            },
          },
        },
        series: [
          {
            //这里的配置显示数值
            label: {
              normal: {
                show: true,
                textStyle: {
                  color: this.color, //雷达图数值颜色
                },
                formatter: function (params) {
                  return params.value;
                },
              },
            },
            type: "radar",
            areaStyle: {
              normal: {
                color: this.color, //改变区域颜色
              },
            }, //背景色显示
            itemStyle: {
              normal: {
                color: this.color, //改变折线点的颜色
                lineStyle: {
                  color: this.color, //改变折线颜色
                },
              },
            },
            data: [
              {
                // value: [70, 60, 50, 55, 75],
                value: this.yDataArr,
              },
            ],
          },
        ],
      };
      myChart.setOption(option);
    },
  },
};
</script>

<style scoped>
</style>
