<template>
  <div id="app">
    <!-- 我需要只显示可视区域 -->
    <!-- 告诉我的；列表每一项多高，因为我要算出一个滚动条来 -->
    <virtual-list :size="40" :remain="8" :items="items" :variable="true">
      <item slot-scope="{item}" :item="item"></item>
    </virtual-list>
  </div>
</template>
<script>
import VirtualList from './components/virtual-list'
import Item from './components/item'
let items = []
for(let i=0;i<10000;i++){
  items.push({
    id:i,
    value:i
  })
}
export default {
  components:{
    VirtualList,
    Item
  },
  data(){
    return{
      items:items,
    }
  }
}
</script>
<style lang="less">
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
#nav {
  padding: 30px;
  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
