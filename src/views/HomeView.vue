<template>
  <div class="hello">

    <div style="display: flex; justify-content: center" >
      <el-tabs v-model="activeName">
        <el-tab-pane label="新闻" name="first"></el-tab-pane>
        <el-tab-pane label="统计" name="second"></el-tab-pane>
        <el-tab-pane label="回马枪" name="three"></el-tab-pane>
      </el-tabs>
    </div>


    <div style="padding: 10px" v-if="activeName == 'first'">
        <div class="item" v-for="(item, index) in news" :key="index">
          <div style="margin-bottom: 10px; ">
              <div>
                <a target="_blank" :href="'https://data.eastmoney.com/notices/detail/' + item.stock_code + '/' + item._id  + '.html'">{{ item.notice_title }}</a>
              </div>

          </div>
          <div style="display: flex; justify-content: space-between; margin-top:20px">
              <div>{{ item.notice_time }}</div>
              <div >
                <a target="_blank" :href="'https://xueqiu.com/S/' + item.area + item.stock_code">{{ item.stock_name }}</a>
              </div>
          </div>
        </div>
        <div class="pagination">
          <el-pagination background layout="prev, pager, next" :total="total" @current-change="currentChange" />
        </div>

    </div>
    <div v-if="activeName == 'second'" style="margin-top: 50px">
      <el-row>
        <el-col :span="8">
          <div style="display: flex; justify-content: center; align-items: center; flex-direction: column" >
            <div>首板</div>
            <div style="display: flex; flex-wrap: wrap; margin-top: 20px">
               <div v-for="(item, index) of one_plate" :key="index" style="margin-left: 10px; width: 100px; margin-top: 5px">
                 <a target="_blank" :href="'https://xueqiu.com/S/' + item.stock_area + item.stock_code">{{ item.stock_name }}</a>
              </div>
            </div>

          </div>

        </el-col>
        <el-col :span="8">
          <div style="display: flex; justify-content: center; align-items: center; flex-direction: column" >
            <div style="margin-bottom: 20px">2连板</div>
              <div v-for="(item, index) of two_plate" :key="index" style="margin-left: 10px; width: 100px; margin-top: 5px">
              <a target="_blank" :href="'https://xueqiu.com/S/' + item.stock_area + item.stock_code">{{ item.stock_name }}</a>
              </div>
          </div>
        </el-col>
        <el-col :span="8">
          <div style="display: flex; justify-content: center; align-items: center; flex-direction: column" >
            <div style="margin-bottom: 20px">3连板</div>
              <div v-for="(item, index) of three_plate" :key="index" style="margin-left: 10px; width: 100px; margin-top: 5px">
              <a target="_blank" :href="'https://xueqiu.com/S/' + item.stock_area + item.stock_code">{{ item.stock_name }}</a>
              </div>
          </div>
        </el-col>
      </el-row>
    </div>

    <div v-if="activeName == 'three'" style="margin-top: 50px">
      <el-row>
        <el-col :span="3">
          <div style="display: flex; justify-content: center; align-items: center; flex-direction: column" >
            <div style="margin-bottom: 20px">2天</div>
              <div v-for="(item, index) of two_plate_c" :key="index" style="margin-left: 10px; width: 100px; margin-top: 5px">
              <a target="_blank" :href="'https://xueqiu.com/S/' + item.stock_area + item.stock_code">{{ item.stock_name }}</a>
              </div>
          </div>
        </el-col>
        <el-col :span="3">
          <div style="display: flex; justify-content: center; align-items: center; flex-direction: column" >
            <div style="margin-bottom: 20px">3天</div>
              <div v-for="(item, index) of three_plate_c" :key="index" style="margin-left: 10px; width: 100px; margin-top: 5px">
              <a target="_blank" :href="'https://xueqiu.com/S/' + item.stock_area + item.stock_code">{{ item.stock_name }}</a>
              </div>
          </div>
        </el-col>

        <el-col :span="3">
          <div style="display: flex; justify-content: center; align-items: center; flex-direction: column" >
            <div style="margin-bottom: 20px">4天</div>
              <div v-for="(item, index) of four_plate" :key="index" style="margin-left: 10px; width: 100px; margin-top: 5px">
              <a target="_blank" :href="'https://xueqiu.com/S/' + item.stock_area + item.stock_code">{{ item.stock_name }}</a>
              </div>
          </div>
        </el-col>
        <el-col :span="3">
          <div style="display: flex; justify-content: center; align-items: center; flex-direction: column" >
            <div style="margin-bottom: 20px">5天</div>
              <div v-for="(item, index) of five_plate" :key="index" style="margin-left: 10px; width: 100px; margin-top: 5px">
              <a target="_blank" :href="'https://xueqiu.com/S/' + item.stock_area + item.stock_code">{{ item.stock_name }}</a>
              </div>
          </div>
        </el-col>


        <el-col :span="3">
          <div style="display: flex; justify-content: center; align-items: center; flex-direction: column" >
            <div style="margin-bottom: 20px">6天</div>
              <div v-for="(item, index) of six_plate" :key="index" style="margin-left: 10px; width: 100px; margin-top: 5px">
              <a target="_blank" :href="'https://xueqiu.com/S/' + item.stock_area + item.stock_code">{{ item.stock_name }}</a>
              </div>
          </div>
        </el-col>
        <el-col :span="3">
          <div style="display: flex; justify-content: center; align-items: center; flex-direction: column" >
            <div style="margin-bottom: 20px">7天</div>
              <div v-for="(item, index) of seven_plate" :key="index" style="margin-left: 10px; width: 100px; margin-top: 5px">
              <a target="_blank" :href="'https://xueqiu.com/S/' + item.stock_area + item.stock_code">{{ item.stock_name }}</a>
              </div>
          </div>
        </el-col>
      <el-col :span="3">
        <div style="display: flex; justify-content: center; align-items: center; flex-direction: column" >
          <div style="margin-bottom: 20px">8天</div>
            <div v-for="(item, index) of eight_plate" :key="index" style="margin-left: 10px; width: 100px; margin-top: 5px">
            <a target="_blank" :href="'https://xueqiu.com/S/' + item.stock_area + item.stock_code">{{ item.stock_name }}</a>
            </div>
        </div>
      </el-col>
      <el-col :span="3">
        <div style="display: flex; justify-content: center; align-items: center; flex-direction: column" >
          <div style="margin-bottom: 20px">9天</div>
            <div v-for="(item, index) of nine_plate" :key="index" style="margin-left: 10px; width: 100px; margin-top: 5px">
            <a target="_blank" :href="'https://xueqiu.com/S/' + item.stock_area + item.stock_code">{{ item.stock_name }}</a>
            </div>
        </div>
      </el-col>


      </el-row>
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
      activeName: 'first',
      one_plate : [],
      two_plate : [],
      three_plate : [],


      two_plate_c : [],
      three_plate_c : [],
      four_plate : [],
      five_plate : [],
      six_plate : [],
      seven_plate : [],
      eight_plate : [],
      nine_plate : [],
      ten_plate : []

    }
  },
  created() {
    this.getNews()
    this.statistics()
    this.statistics_huimaqiang()
  },
  methods: {

    getNews(){
      let that= this
      axios.get('/api/news', {
        params: {
            page: this.page        // 参数 firstName
        }
      })
      .then(function (response) {
        that.total = response.data.total
        that.news = response.data.list
      })
      .catch(function (error) {
        console.log(error);
      });
    },

    statistics(){
      let that= this
      axios.get('/api/statistics')
      .then(function (response) {
        console.log(response)
        that.one_plate = response.data.one_plate
        that.two_plate = response.data.two_plate
        that.three_plate = response.data.three_plate
      })
      .catch(function (error) {
        console.log(error);
      });
    },
    statistics_huimaqiang(){
      let that= this
      axios.get('/api/huimaq')
      .then(function (response) {
        that.two_plate_c = response.data.two_plate
        that.three_plate_c = response.data.three_plate
        that.four_plate = response.data.four_plate
        that.five_plate = response.data.five_plate
        that.six_plate = response.data.six_plate
        that.seven_plate = response.data.seven_plate
        that.eight_plate = response.data.eight_plate
        that.nine_plate = response.data.nine_plate
        that.ten_plate = response.data.ten_plate
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
