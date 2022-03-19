<template>


  <div>
    <div>
      <h1 class="txt4">股票数据可视化</h1>
    </div>
    <el-row>
      <el-col :xs="5" :sm="5" :md="5" :lg="5" :xl="1">
        <div>
            <h3 class="txt4">股票名称</h3>
          <div>
            <el-select v-model="value" filterable placeholder="请选择">
              <el-option
                v-for="item in options"
                :key="item.value"
                :label="item.label"
                :value="item.label"
                >

              </el-option>
            </el-select>
          </div>
          <br>
          <div>
            <el-input
              placeholder="请输入内容"
              v-model="value"
              clearable
            >
            </el-input>
          </div>
        </div>
      </el-col>
      <el-col :xs="19" :sm="19" :md="19" :lg="19" :xl="23">
        <div>
          <el-card shadow="always">
            <div>
              <LineChart v-bind:namejson="value"></LineChart>
            </div>
          </el-card>

            <el-divider ></el-divider>
          <el-card>
            <div>
              <OHLC v-bind:namejson="value"></OHLC>
            </div>
          </el-card>

          </div>
      </el-col>
    </el-row>
  </div>


</template>

<script>
import axios from "axios";
import LineChart from "./LineChart";
import OHLC from "./OHLC";

export default {
  name: 'HelloWorld',
  data () {
    return {
      options: [{
        value: '选项1',
        label: '万华化学'
      }, {
        value: '选项2',
        label: '上海能源'
      }, {
        value: '选项3',
        label: '世名科技'
      }, {
        value: '选项4',
        label: '中国动力'
      }, {
        value: '选项5',
        label: '中新药业'
      },{
        value: '选项6',
        label: '万里马'
      }, {
        value: '选项7',
        label: '三元股份'
      }, {
        value: '选项8',
        label: '三德科技'
      }, {
        value: '选项9',
        label: '上海家化'
      },{
        value: '选项10',
        label: '中文传媒'
      }, {
        value: '选项11',
        label: '中油工程'
      }, {
        value: '选项12',
        label: '久吾高科'
      }, {
        value: '选项13',
        label: '乐心医疗'
      },{
        value: '选项14',
        label: '五洲交通'
      }, {
        value: '选项15',
        label: '亚宝药业'
      }, {
        value: '选项16',
        label: '交大昂立'
      }, {
        value: '选项17',
        label: '今天国际'
      }],
      value: '',
      namejson:''
    }
  },

  mounted() {
    // axios.get('../../static/'+this.name+'.json').then(response => {
    //     this.msg = response.data;
    //     for(var i=0;i<response.data.length;i++) {
    //       this.datalist[i] = response.data[i].交易日期;
    //     }
    // }, response => {
    //   console.log("error");
    // });
  },
  components: {
    OHLC,
    LineChart
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
.el-card{
  box-shadow: 5px 5px 5px 5px rgb(116, 114, 114) !important;
}
.txt4{
  background: linear-gradient(to bottom, #c0c0c4, #282727);
  -webkit-text-fill-color: transparent;
  -webkit-background-clip: text;
}
.el-input__inner {
  background-color: #c7c9c9;
  width: 180px;
}
</style>

