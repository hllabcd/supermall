<template>
  <div class="tabControl">
    <div v-for="(item,index) in titles"
         class="tabControl-item"
         :class="{active:index === currentIndex}" @click="itemclick(index)">
      <span>{{item}}</span>
    </div>
  </div>
</template>

<script>
  export default {
    name: "TabControl",
    data(){
      return {
        currentIndex:0

      }
    },
    props:{
      titles:{
        type:Array,
        default(){
          return []
        }
      }
    },
    methods:{
      itemclick(index){
        this.currentIndex=index
        this.$emit('tabclick',index)
      }
    }
  }
</script>

<style scoped>
   .tabControl{
     display:flex;
     text-align: center;
     /*height: 40px;*/
     line-height: 40px;
     font-size: 15px;
     background-color: #fff;
   }
  .tabControl-item{
    flex: 1;

  }
  .active{
    color: var(--color-high-text);
  }
  .active span{
    border-bottom: 3px solid var(--color-tint);
    padding: 5px;
  }
</style>
