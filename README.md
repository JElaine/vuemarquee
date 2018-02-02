# vuemarquee

> 基于vue2的垂直跑马灯

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report
```

For a detailed explanation on how things work, check out the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).

#### 在浏览器打开 http://localhost:8083/#/demo1 或者 http://localhost:8083/#/demo2

demo1是非常简单的一个例子,在demo1中，直接将组件中的源代码引入，而不是直接使用插件，效果是一样的，只是方便调试

```
listData: ['消息1', '消息2', '消息3', '消息4'],
reverseData: ['消息4', '消息3', '消息2', '消息1'] 
```

```
<div><h2>向上</h2>
  <VueMarquee :duration="600" :interval="2000">
    <li v-for="i in listData">{{i}}</li>
  </VueMarquee>

  <div style="margin-top: 100px"></div>
  <h2>向下</h2>
  <VueMarquee :duration="600" :interval="2000" :direction="'down'">
    <li v-for="i in reverseData">{{i}}</li>
  </VueMarquee>
</div>
```
#### demo2是从远程获取数据后再显示，使用vue-marquee插件
  由于从远程获取数据是异步，页面渲染完成，但是数据有可能还没获取到，此时就会出错，所以在此可以在数据还没获取到的时候不渲染组件，用vue中的v-if阻止组件的渲染，等到数据取回时再渲染组件
  ##### 此接口为知乎公开接口，一般的浏览器会有跨域安全问题，所以在开发过程中需要设置浏览器的跨域安全，可以参考https://github.com/zhongxia245/blog/issues/28

  ```
  <h2>向上</h2>
  <Marquee v-if="showHint" :duration="600" :interval="2000">
    <li v-for="i in reverseData">{{i.title}}</li>
  </Marquee>
  ```
  ```
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
  ```

