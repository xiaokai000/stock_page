<template>
  <div class="hello">

    <el-row>
      <el-col :span="4"><div class="grid-content bg-purple" /></el-col>
      <el-col :span="16"><div class="grid-content bg-purple-light" />
          <div style="padding: 40px">
            <div class="item" v-for="(item, index) in news" :key="index">
              <div style="margin-bottom: 10px; display: flex; justify-content: space-between;">
                  <div>
                    <a target="_blank" :href="'https://data.eastmoney.com/notices/detail/' + item.stock_code + '/' + item._id  + '.html'">{{ item.notice_title }}</a>
                  </div>
                  <div>{{ item.notice_time }}</div>
              </div>
              <div style="display: flex; justify-content: flex-end;">
                  <div style="color:blue">
                    <a target="_blank" :href="'https://xueqiu.com/S/' + item.area + item.stock_code">{{ item.stock_name }}</a>
                  </div>
              </div>
            </div>
            <div class="pagination">
              <el-pagination background layout="prev, pager, next" :total="total" @current-change="currentChange" />
            </div>
            
          </div>
           
      </el-col>
      <el-col :span="4"><div class="grid-content bg-purple" /></el-col>
    </el-row>

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
      total: 0
    }
  },
  created() {
    this.getNews()
  },
  methods: {

    getNews(){
      let that= this
      axios.get('http://127.0.0.1:15006/', { 
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
  height: 50px;
  margin: 20px;

}
.pagination{
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
