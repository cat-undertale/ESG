<template>
  <div className="Echarts">
    <div id="main1" style="width: 1290px;height:500px;"></div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "Echarts",
  data () {
    return {
      date:[],
      data:[],
      name: 'sh600432',
      test: ''
    }
  },
  props:{
    namejson: {
      type:String,
      required: true
    }
  },
  watch:{
    namejson:{
      handler(n,o){
        this.test = n
      },
      deep: true
    }
  },
  methods: {
    myEcharts() {
      var myChart = this.$echarts.init(document.getElementById('main1'));

      var option = {
        title: {
          left: 'center',
          text: this.test+"股票K线图"
        },
        xAxis: {
          data: this.date
        },
        yAxis: {},
        tooltip: {
          trigger: 'axis',
          axisPointer: {
            type: 'line'
          }
        },
        series: [
          {
            type: 'candlestick',
            data: this.data
            // data: [
            //   [20, 34, 10, 38],
            //   [40, 35, 30, 50],
            //   [31, 38, 33, 44],
            //   [38, 15, 5, 42]
            // ]
          }
        ]
      };
      myChart.setOption(option);
    }
  },
  created() {
    this.timer = setInterval(() => {
      axios.get('../../static/all_json/'+this.test+'.json').then(response => {
        // console.log(response.data.RECORDS[1].开盘价);
        // console.log(response.data.RECORDS[1].收盘价);
        // console.log(response.data.RECORDS[1].最低价);
        // console.log(response.data.RECORDS[1].最高价);

        for(var i=0;i<response.data.RECORDS.length;i++) {
          this.date[i] = response.data.RECORDS[i].交易日期;

          var b = [];//辅助数组
          b[0] = response.data.RECORDS[i].开盘价;
          b[1] = response.data.RECORDS[i].收盘价;
          b[2] = response.data.RECORDS[i].最低价;
          b[3] = response.data.RECORDS[i].最高价;
          this.data[i] = b;
        }
        // for(var i=0;i<response.data.RECORDS.length;i++) {
        //     this.date[i] = response.data.RECORDS[i].交易日期;
        //     this.data[i] = parseInt(response.data.RECORDS[i].成交量);
        //   }
        this.myEcharts();

      }, response => {
        console.log("error");
      });
    })
  },
  beforeDestroy() {
    clearInterval(this.timer)
  },
}
</script>

<style scoped>

</style>
