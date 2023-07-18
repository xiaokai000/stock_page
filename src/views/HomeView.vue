<template>
  <div class="hello">

    <div style="display: flex; justify-content: center; align-items:center">
      <el-tabs v-model="activeName">
        <el-tab-pane label="最近涨停" name="1"></el-tab-pane>
        <el-tab-pane label="回马枪" name="2"></el-tab-pane>
        <el-tab-pane label="十字星" name="3"></el-tab-pane>
        <el-tab-pane label="下影线" name="4"></el-tab-pane>
        <el-tab-pane label="连续上涨" name="5"></el-tab-pane>
        <el-tab-pane label="底部大涨" name="6"></el-tab-pane>

      </el-tabs>
    </div>

    <div>
      <div style="margin-top: 50px; padding: 0px 150px">

        <div v-for="(item, index) of array"
          style="display: flex; justify-content: flex-start; align-items:flex-start; flex-wrap: wrap;">
          <a target="_blank" :href="'https://xueqiu.com/S/' + item.stock_area + item.stock_code">

          <div>
            <span style="margin-right: 5px" :class="{ 'black': item.stock_code.startsWith('3') }">{{ item.stock_name
            }}</span>
            <span :class="{ 'red': item.pctChg > 0, 'green': item.pctChg < 0 }">{{ item.pctChg }}</span>
          </div>
          </a>
          <div :id="item.stock_code" style="width: 100px; height: 100px;"></div>
        </div>
      </div>
    </div>


  </div>
</template>

<script>
import axios from 'axios'
import * as echarts from 'echarts';

export default {
  name: 'HelloWorld',
  data() {
    return {
      activeName: '1',
      zhangting_data: [],
      huimaq_data: [],
      shizixing_data: [],
      xiayingxian_data: [],
      lianxu_data: [],
      dibu_data: [],
      host: 'http://121.4.102.234:8080',
      // host: '',
      Intervalid: '',
      array: []

    }
  },

  beforeDestroy() {
    clearInterval(this.Intervalid)
  },

  created() {
    this.getData()
    this.Intervalid = setInterval(() => {
      this.getData()
    }, 2000)
    setTimeout(() => {
      this.array = this.zhangting_data
    },500)

    setTimeout(() => {
      this.initChartDom()
    },500)

  },
  watch: {
    activeName(newValue, oldValue) {

      const fruits = new Map([
        ["1", this.zhangting_data],
        ["2", this.huimaq_data],
        ["3", this.shizixing_data],
        ["4", this.xiayingxian_data],
        ["5", this.lianxu_data],
        ["6", this.dibu_data],
      ]);
      this.array = fruits.get(newValue)
      

    }
  },
  methods: {


    getData(){
      this.getZhangting()
      this.getHuimaqiang()
      this.getShiZiXing()
      this.getXiaYingXian()
      this.lianxu()
      this.getDibu()
    },

    initChartDom(){

      let tmp = []
      tmp = tmp.concat(this.zhangting_data)
      tmp = tmp.concat(this.huimaq_data)
      tmp = tmp.concat(this.shizixing_data)
      tmp = tmp.concat(this.xiayingxian_data)
      tmp = tmp.concat(this.lianxu_data)
      tmp = tmp.concat(this.dibu_data)

      for (let x of tmp){
        var chartDom = document.getElementById(x.stock_code);
        console.log(chartDom)
          var myChart = echarts.init(chartDom);
          var option;
          
          x.chartDom = chartDom

          option = {
            xAxis: {
              data: ['2017-10-24', '2017-10-25', '2017-10-26', '2017-10-27']
            },
            yAxis: {},
            series: [
              {
                type: 'candlestick',
                data: [
                  [20, 34, 10, 38],
                  [40, 35, 30, 50],
                  [31, 38, 33, 44],
                  [38, 15, 5, 42]
                ]
              }
            ]
          };
          myChart.setOption(option);
      }
    },

    getZhangting() {
      let that = this
      axios.get(that.host + '/api/zhangting')
        .then(function (response) {
          that.zhangting_data = response.data
        })
    },
    getDibu() {
      let that = this
      axios.get(that.host + '/api/dibu')
        .then(function (response) {
          that.dibu_data = response.data
        })
    },
    getShiZiXing() {
      let that = this
      axios.get(that.host + '/api/shizixing')
        .then(function (response) {
          that.shizixing_data = response.data
        })
    },

    getXiaYingXian() {
      let that = this
      axios.get(that.host + '/api/xiayingxian')
        .then(function (response) {
          that.xiayingxian_data = response.data
        })
    },


    getHuimaqiang() {
      let that = this
      axios.get(that.host + '/api/huimaq')
        .then(function (response) {
          that.huimaq_data = response.data
        })

    },
    lianxu() {
      let that = this
      axios.get(that.host + '/api/lianxu')
        .then(function (response) {
          that.lianxu_data = response.data
        })

    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {

  text-decoration: none;
}

a,
a:hover,
a:active {

  color: #0000FF;

}

.item {
  border-radius: 10px;
  background: #DCDCDC;
  padding: 10px 30px;

  margin: 20px;

}

.pagination {
  display: flex;
  justify-content: center;
  align-items: center;

}

.red {
  color: red;
}

.green {
  color: green;
}

.black {
  color: #EE9A00;
}
</style>
