<template>
  <div class="wrapper" ref="wrapper">
    <div class="content">
      <slot></slot>
    </div>
  </div>
</template>

<script>
import BScroll from 'better-scroll';

export default {
  name:'Scroll',
  props:{
    probeType:{
      type:Number,
      default:0
    },
    pullUpLoad:{
      type: Boolean,
      default: false
    }
  },
  components: {},
  data() {
    return {
      scroll: null
    };
  },
  computed: {},
  created() {},
  mounted() {
    // 1.创建better-scroll对象
    this.scroll = new BScroll(this.$refs.wrapper,{
      click: true,
      probeType:this.probeType,
      pullUpLoad: this.pullUpLoad,
      observeDOM : true
    })
    // 2.监听滚动的位置
    if(this.probeType === 2 || this.probeType === 3){
      this.scroll.on('scroll',(position) =>{
        // console.log(position);
        //发出去
        this.$emit('scroll',position)
      })
    }

    // this.scroll.refresh()

    //3.监听上拉事件
    if(this.pullUpLoad){
      this.scroll.on('pullingUp',()=>{
        // console.log("上拉加载");
        setTimeout(() => {
          this.scroll.finishPullUp()
        }, 2000);
        // 发出去
        this.$emit('pullingUp')
      })
    }
    
  },
  methods: {
    scrollTo(x, y, time = 800){
      this.scroll && this.scroll.scrollTo(x, y, time)
    },
    refresh(){
      // console.log('-------');
      this.scroll && this.scroll.refresh()
    },
    finishPullUp(){
      this.scroll && this.scroll.finishPullUp()
    },
    getScrollY(){
      return this.scroll ? this.scroll.y : 0
    }
  }
}
</script>
<style scoped>
/* .wrapper{ */
  /* height: calc(); */
  /* position: relative; */
/* } */
</style>