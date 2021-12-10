<template>

    <div class="goods-list">
      <GoodsListItem
        v-for="item in goodslist"
        :goodslistitem="item"
        class="item"></GoodsListItem>
    </div>

</template>

<script>
  import GoodsListItem from "./GoodsListItem";
  export default {
    name: "GoodList",
    components:{
      GoodsListItem
    },
    props:{
        goodslist:{
          type:Array,
          default(){
            return []
          }
        }
    }
  }
</script>

<style scoped>
  .goods-list {
    display: flex;
    flex-wrap: wrap;
    /*padding: 5px;*/
    justify-content: space-around;

  }

  .goods-list .item {
    width: 40%;
  }
</style>
