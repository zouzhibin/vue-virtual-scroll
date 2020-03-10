<template>
<!-- 能滚动的盒子 -->
    <div class="viewport" ref="viewport" @scroll="handleScroll">
         <!-- 自己做一个滚动条    -->
         <div class="scroll-bar" ref="scrollBar"></div>
         <!-- 真实渲染的内容 -->
         <div class="scroll-list" :style="{transform:`translate3d(0,${offset}px,0`}">
             <div v-for="item in visibleData" :key="item.id" :iid="item.id">
                 <slot :item="item"></slot>
             </div>

         </div>
    </div>
</template>
<script>
export default{
    props:{
        size:Number, // 当前每一项的高度
        remain:Number, // 可见多少个
        items:Array
    },
    data(){
      return {
          start:0,
          end:this.remain,
          offset:0
      }
    },
    computed:{
       //渲染三屏幕
       prevCount(){
         return Math.min(this.start,this.remain)
       },
       nextCount(){ // 后面预留几个
          return Math.min(this.remain,this.items.length-this.end)
      },
      // 可见的数据有哪些
       visibleData(){
           let start = this.start-this.prevCount
           let end = this.end+this.nextCount
           console.log('start,end',start,end,this.start,this.end,this.items.length)
           return this.items.slice(start,end)
       }
    },
    mounted(){
        this.$refs.viewport.style.height = this.size*this.remain+'px'
        this.$refs.scrollBar.style.height = this.items.length*this.size+'px'
    },
    methods:{
        handleScroll() {
            // 1.应该先算出来滚过去几个了，当前 应该从第几个开始显示
            let scrollTop = this.$refs.viewport.scrollTop
            // 获取当前应该从第几个开始渲染
            this.start = Math.floor(scrollTop / this.size)
            // console.log('this.start ',this.start)
            // 3.在计算当前结尾的位置
            this.end = this.start + this.remain; // 当前可渲染的区域
            // 定位当前的可视区域，让当前渲染的内容在当前的viewport的可视区域内
            // 如果有预留渲染 ，应该把这个位置在向上偏移多少
            this.offset = this.start*this.size - this.size*this.prevCount // 让可视区域去调整位置
        }
    }
}
</script>
<style>
    .viewport{
        overflow-y: scroll;
        width: 100%;
        position: relative;
    }
    .scroll-list{
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
    }
</style>
