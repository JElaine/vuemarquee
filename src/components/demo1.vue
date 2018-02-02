<template>
  <div class="hello">
    <div><h2>向上</h2>
    <VueMarquee :duration="600" :interval="2000">
      <li v-for="i in listData">{{i}}</li>
    </VueMarquee>

    <div style="margin-top: 100px"></div>
    <h2>向下</h2>
    <VueMarquee :duration="600" :interval="2000" :direction="'down'">
      <li v-for="i in reverseData">{{i}}</li>
    </VueMarquee></div>
  </div>
</template>

<script>
import { VueMarquee } from './export.js'
export default {
  name: 'HelloWorld',
  components: {
    VueMarquee
  },
  data () {
    return {
      listData: ['消息1', '消息2', '消息3', '消息4'],
      reverseData: ['消息4', '消息3', '消息2', '消息1'] 
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
