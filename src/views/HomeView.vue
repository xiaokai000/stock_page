<template>
  <div class="hello">

    <div style="display: flex; justify-content: center; align-items:center" >
      <el-tabs v-model="activeName">
        <el-tab-pane label="最近涨停" name="first"></el-tab-pane>
        <el-tab-pane label="连扳" name="second"></el-tab-pane>
        <el-tab-pane label="回马枪" name="three"></el-tab-pane>
        <el-tab-pane label="十字星" name="four"></el-tab-pane>
        <el-tab-pane label="下影线" name="five"></el-tab-pane>
        <el-tab-pane label="周线十字星" name="six"></el-tab-pane>
        <el-tab-pane label="底部大涨" name="seven"></el-tab-pane>
        <el-tab-pane label="连续上涨" name="eight"></el-tab-pane>
      </el-tabs>
    </div>


    <div style="padding: 0px 300px" v-if="activeName == 'first'">
      <div style="display: flex; justify-content: space-around; align-items:flex-start">

        <div v-for="(item, index) of zhangting_data">
          <div style="display: flex; justify-content: center; align-items: center; flex-direction: column" >
            <div style="margin-bottom: 20px">{{ item.label }}</div>
              <div v-for="(item, index) of item.value" :key="index" style="margin-top: 5px">
              <a target="_blank" :href="'https://xueqiu.com/S/' + item.stock_area + item.stock_code">{{ item.stock_name }}</a>
              </div>
          </div>
        </div>

      </div>

    </div>
    <div v-if="activeName == 'second'" style="margin-top: 50px; padding: 0px 300px">
      <div style="display: flex; justify-content: space-around; align-items:flex-start">

        <div v-for="(item, index) of lianban_data">
          <div style="display: flex; justify-content: center; align-items: center; flex-direction: column" >
            <div style="margin-bottom: 20px">{{ item.label }}</div>
              <div v-for="(item, index) of item.value" :key="index" style="margin-top: 5px">
              <a target="_blank" :href="'https://xueqiu.com/S/' + item.stock_area + item.stock_code">{{ item.stock_name }}</a>
              </div>
          </div>
        </div>

      </div>
    </div>

    <div v-if="activeName == 'three'" style="margin-top: 50px; padding: 0px 100px">
      <div style="display: flex; justify-content: space-around; align-items:flex-start">

        <div v-for="(item, index) of huimaq_data">
          <div style="display: flex; justify-content: center; align-items: center; flex-direction: column" >
            <div style="margin-bottom: 20px">{{ item.label }}</div>
              <div v-for="(item, index) of item.value" :key="index" style="margin-top: 5px">
              <a target="_blank" :href="'https://xueqiu.com/S/' + item.stock_area + item.stock_code">{{ item.stock_name }}</a>
              </div>
          </div>
        </div>

      </div>
    </div>

    <div v-if="activeName == 'four'" style="margin-top: 50px; padding: 0px 450px">

      <div v-for="(item, index) of shizixing_data" style="display: flex; justify-content: space-around; align-items:flex-start; flex-wrap: wrap;">

          <div v-for="(item, index) of item.value" :key="index" style="margin: 15px">
          <a target="_blank" :href="'https://xueqiu.com/S/' + item.stock_area + item.stock_code">{{ item.stock_name }}</a>
          </div>

      </div>

  </div>

    <div v-if="activeName == 'five'" style="margin-top: 50px; padding: 0px 100px">
      <div style="display: flex; justify-content: space-around; align-items:flex-start">

        <div v-for="(item, index) of xiayingxian_data">
          <div style="display: flex; justify-content: center; align-items: center; flex-direction: column" >
            <div style="margin-bottom: 20px">{{ item.label }}</div>
              <div v-for="(item, index) of item.value" :key="index" style="margin-top: 5px">
              <a target="_blank" :href="'https://xueqiu.com/S/' + item.stock_area + item.stock_code">{{ item.stock_name }}</a>
              </div>
          </div>
        </div>

      </div>
    </div>

    <div v-if="activeName == 'six'" style="margin-top: 50px; padding: 0px 450px">

        <div v-for="(item, index) of zhouxian_shizixing_data" style="display: flex; justify-content: space-around; align-items:flex-start; flex-wrap: wrap;">

            <div v-for="(item, index) of item.value" :key="index" style="margin: 15px">
            <a target="_blank" :href="'https://xueqiu.com/S/' + item.stock_area + item.stock_code">{{ item.stock_name }}</a>
            </div>

        </div>

    </div>

    <div v-if="activeName == 'seven'" style="margin-top: 50px; padding: 0px 100px">
      <div style="display: flex; justify-content: space-around; align-items:flex-start">

        <div v-for="(item, index) of dibu_data">
          <div style="display: flex; justify-content: center; align-items: center; flex-direction: column" >
            <div style="margin-bottom: 20px">{{ item.label }}</div>
              <div v-for="(item, index) of item.value" :key="index" style="margin-top: 5px">
              <a target="_blank" :href="'https://xueqiu.com/S/' + item.stock_area + item.stock_code">{{ item.stock_name }}</a>
              </div>
          </div>
        </div>

      </div>
    </div>

    <div v-if="activeName == 'eight'" style="margin-top: 50px; padding: 0px 100px">
      <div v-for="(item, index) of lianxu_data" style="display: flex; justify-content: space-around; align-items:flex-start; flex-wrap: wrap;">

        <div v-for="(item, index) of item.value" :key="index" style="margin: 15px">
        <a target="_blank" :href="'https://xueqiu.com/S/' + item.stock_area + item.stock_code">{{ item.stock_name }}</a>
        </div>

    </div>
    </div>

  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'HelloWorld',
  data() {
    return {
      news: [],
      page: 1,
      total: 0,
      activeName: 'second',

      zhangting_data: [],
      lianban_data: [],
      huimaq_data: [],
      shizixing_data: [],
      xiayingxian_data: [],
      zhouxian_shizixing_data: [],
      dibu_data: [],
      lianxu_data:[]

    }
  },
  created() {
    this.getNews()
    this.statistics()
    this.statistics_huimaqiang()
    this.getShiZiXing()
    this.getXiaYingXian()
    this.getZhouShiZiXing()
    this.getDiBu()
    this.getLianXu()
  },
  methods: {

    getNews(){
      let that= this
      axios.get('/api/zhangting')
      .then(function (response) {
        that.zhangting_data = response.data

      })
      .catch(function (error) {
        console.log(error);
      });
    },
    getShiZiXing(){
      let that= this
      axios.get('/api/shizixing')
      .then(function (response) {
        that.shizixing_data = response.data

      })
      .catch(function (error) {
        console.log(error);
      });
    },
    getZhouShiZiXing(){
      let that= this
      axios.get('/api/zhouxian_shizixing')
      .then(function (response) {
        that.zhouxian_shizixing_data = response.data

      })
      .catch(function (error) {
        console.log(error);
      });
    },
    getXiaYingXian(){
      let that= this
      axios.get('/api/xiayingxian')
      .then(function (response) {
        that.xiayingxian_data = response.data

      })
      .catch(function (error) {
        console.log(error);
      });
    },

    statistics(){
      let that= this
      axios.get('/api/lianban')
      .then(function (response) {
        console.log(response)
        that.lianban_data = response.data

      })
      .catch(function (error) {
        console.log(error);
      });
    },
    statistics_huimaqiang(){
      let that= this
      axios.get('/api/huimaq')
      .then(function (response) {
        that.huimaq_data = response.data
        
      })
      .catch(function (error) {
        console.log(error);
      });
    },
    getDiBu(){
      let that= this
      axios.get('/api/dibu')
      .then(function (response) {
        that.dibu_data = response.data
        
      })
      .catch(function (error) {
        console.log(error);
      });
    },
    getLianXu(){
      let that= this
      axios.get('/api/lianxu')
      .then(function (response) {
        that.lianxu_data = response.data
        
      })
      .catch(function (error) {
        console.log(error);
      });
    },

    currentChange(e){
        console.log('当前页:', e)
        this.page = e
        this.getNews()
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

.item {
  border-radius: 10px;
  background: 	#DCDCDC;
  padding: 10px 30px;

  margin: 20px;

}
.pagination{
  display: flex;
  justify-content: center;
  align-items: center;

}
</style>
