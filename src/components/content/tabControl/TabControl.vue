<template>
  <div class="tab-control">
      <div v-for="(item,index) in titles"
       :key="index" class="tab-control-item"
        :class="{active: index === currentIndex}" @click="itemClick(index)">
          <span>{{item}}</span>
      </div>
  </div>
</template>

<script>
export default {
    name:"TabControl",
    props:{
        titles:{
           type:Array,
           default(){
               return{
                   
               }
           } 
        }
    },
    data(){
        return {
            currentIndex:0
        }
    },
    methods:{
        itemClick(index){
            this.currentIndex = index;
            this.$emit('tabClick',index)
        }
    }
}
</script>

<style>
    .tab-control{
        display: flex;
        text-align: center;
        font-size: 15px;
        background-color:#fff;
        height: 40px;
        line-height: 40px;
        z-index:9;
    }
    .tab-control-item{
        flex: 1;
        
    }
    .tab-control-item span{
        padding: 5px;
    }
    .active{
        /* color:var(--color-hight-text); */
       color: deeppink;
    }
    .active span{
         /* border-bottom:3px soild var(--color-tint); */
        border-bottom:3px solid deeppink;
    }
    /* 看看有没有错误 */
</style>