<template>
  <div class="hello">
    <div style="margin-top: 100px"></div>
    <h2>向上</h2>
    <Marquee v-if="showHint" :duration="600" :interval="2000">
      <li v-for="i in reverseData">{{i.title}}</li>
    </Marquee>
    </div>
  </div>
</template>

<script>
import Marquee from 'vue-marquee'
import axios from 'axios'
export default {
  name: 'HelloWorld',
  components: {
    Marquee
  },
  data () {
    return {
      listData: ['消息1', '消息2', '消息3', '消息4'],
      reverseData: [],
      showHint: false
    }
  },
  created(){
    this.getList()
  },
  methods: {
    getList(){
      axios.get('https://news-at.zhihu.com/api/4/news/latest')
        .then(response => {
          // console.log(response.data.stories)
          this.reverseData = response.data.stories
          // 等待获取到数据后，再渲染组件
          this.showHint = true
        }).catch(error => {
          console.log(error);
      });
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scope> 
li {
  width: 100%;
  background-color: rgb(180, 180, 178);
  text-align: center;
}
</style>
