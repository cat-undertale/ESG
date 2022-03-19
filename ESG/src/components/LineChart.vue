<template>
  <div className="Echarts">
    <div id="main" style="width: 1290px;height:500px;"></div>
  </div>

</template>

<script>
import axios from "axios";

export default {
  name: 'Echarts',
  data () {
    return {
      datalist:[],
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
      }
      // deep: true
    }
  },

  methods: {
    myEcharts() {
      // 基于准备好的dom，初始化echarts实例
      var myChart = this.$echarts.init(document.getElementById('main'));
      // 指定图表的配置项和数据
      var option = {
        xAxis: {
          type: 'category',
          data: this.datalist

        },
        yAxis: {
          type: 'value'
        },
        tooltip: {
          trigger: 'axis'
        },
        series: [
          {
            data: this.data,
            type: 'line'
          }
        ],
        title: {
            left: 'center',
            text: this.test+'股票成交量'
          }
      };

      // 使用刚指定的配置项和数据显示图表。
      myChart.setOption(option);
    }

  },
  created() {
    this.timer = setInterval(() => {
      axios.get('../../static/all_json/'+this.test+'.json').then(response => {
        for(var i=0;i<response.data.RECORDS.length;i++) {
          this.datalist[i] = response.data.RECORDS[i].交易日期;
          this.data[i] = parseInt(response.data.RECORDS[i].成交量);
        }
        this.myEcharts();

      }, response => {
        console.log("error");
      },1000);
    })
  },
  beforeDestroy() {
    clearInterval(this.timer)
    },
  mounted() {
    console.log(this.test)
    // axios.get('../../static/all_json/'+this.test+'.json').then(response => {
    //     console.log(response.data.RECORDS[1])
    //   for(var i=0;i<response.data.RECORDS.length;i++) {
    //       this.datalist[i] = response.data.RECORDS[i].交易日期;
    //       this.data[i] = parseInt(response.data.RECORDS[i].成交量);
    //     }
    //   this.myEcharts();
    //
    // }, response => {
    //   console.log("error");
    // },1000);


  }
}
</script>

<style>

</style>

