<template>
    <swiper class="detail-swiper">
        <swiper-item v-for="(item,index) in topImages" :key="index">
            <img :src="item" alt="">
        </swiper-item>
    </swiper>
</template>

<script>
import {Swiper, SwiperItem} from 'components/common/swiper/index'

export default {
  name:'DetailSwiper',
  props:{
    topImages: {
        type: Array,
        default () {
            return []
        }
    }
  },
  components: {
    Swiper,
    SwiperItem,
  },
  data() {
    return {};
  },
  computed: {},
  watch: {},
  methods: {},
  created() {}, 
  mounted() {}, 
}
</script>
<style scoped>
.detail-swiper{
    height: 300px;
    overflow: hidden;
}
</style>