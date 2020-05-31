<template>
  <div id="detail">
      <detail-nav-bar class="detail-nav"></detail-nav-bar>
       <scroll class="content" ref="scroll">
        <detail-swiper :top-images="topImages"></detail-swiper>
        <detail-base-info :goods="goods"></detail-base-info>
        <detail-shop-info :shop="shop"></detail-shop-info>
        <!-- <detail-goods-info :detail-info="detailInfo" @imgLoad="imageLoad"></detail-goods-info> -->
       </scroll>
      
  </div>
</template>

<script>
import DetailNavBar from './childComps/DetailNavBar'
import DetailSwiper from './childComps/DetailSwiper'
import DetailBaseInfo from './childComps/DetailBaseInfo'
import DetailShopInfo from './childComps/DetailShopInfo'
// import DetailGoodsInfo from './childComps/DetailGoodsInfo'

import Scroll from 'components/common/scroll/Scroll'

import {getDetail,Goods,Shop} from "network/detail";

export default {
    name:"Detail",
    components:{
      DetailNavBar,
      DetailSwiper,
      DetailBaseInfo,
      DetailShopInfo,
      // DetailGoodsInfo,
      Scroll
    },
    data(){
      return{
        iid:null,
        topImages:[],
        goods:{},
        shop:{},
        detailInfo:{}
      }
    },
    created(){
      //1.保存传入的iid
      this.iid = this.$route.params.iid;
      //2.根据iid请求详情数据
      getDetail(this.iid).then(res =>{
        // console.log(res);
        const data = res.result;
        this.topImages = res.result.itemInfo.topImages

        //2.获取商品信息
        this.goods = new Goods(data.itemInfo,data.columns,data.shopInfo.services)
        
        //3.创建店铺信息的对象
        this.shop = new Shop(data.shopInfo)

        //4.保存商品的详情数据
        this.detailInfo = data.detailInfo;
     })
    },
    methods:{
      imageLoad(){
        this.$refs.scroll.refresh()
      }
    }
}
</script>

<style>
 #detail{
    position: relative;
    z-index: 1;
    background-color: #fff;
    /* height: 100vm; */
    height: 100vh;
  }
 
 /* .detail-nav{
   position: relative;
   z-index: 10;
   background-color: #fff;
 } */
 /* .content{
   height:calc(100% - 44px);
 } */
.content{
  background-color: #fff;
  height: calc(100%,44px);
}

</style>