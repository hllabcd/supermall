<template>
<div id="home">
  <nav-bar class="home-nav">
    <div slot="center">购物街</div>
  </nav-bar>
  <HomeSwiper :banners="banners"></HomeSwiper>
  <recommend-comps :recommends="recommends"></recommend-comps>
  <feature></feature>
  <tab-control :titles="['流行','新款','精选']" class="tabcontrol" @tabclick="tabclick"></tab-control>
  <GoodList :goodslist=showMessage></GoodList>



</div>
</template>
<script>

import HomeSwiper from "./childComps/HomeSwiper";
import RecommendComps from "./childComps/RecommendComps";
import Feature from "./childComps/Feature";

import NavBar from '../../components/common/navbar/NavBar'
import TabControl from "../../components/content/tabControl/TabControl";
import GoodList from "../../components/content/goodList/GoodList";

import { getHomeMultidata,getHomedata} from "../../network/home";


  export default {
    name: "Home",
    components:{
      HomeSwiper,
      RecommendComps,
      Feature,
      NavBar,
      TabControl,
      GoodList
         },
    data(){
      return {
        banners:[],
        recommends:[],
        goods:{
          'pop':{page:0,list:[]},
          'new':{page:0,list:[]},
          'sell':{page:0,list:[]}
        },
        currentType:'pop'
      }
    },
    created() {
      this.getHomeMultidata();
      this.getHomedata('pop');
      this.getHomedata('new');
      this.getHomedata('sell');
    },
    computed:{
      showMessage(){
        return this.goods[this.currentType].list

      }
    },
    methods:{
      //监听事件
      tabclick(index){
        console.log(index);
        switch (index) {
          case 0:
            this.currentType='pop'
            break
          case 1:
            this.currentType='new'
            break
          case 2:
            this.currentType='sell'
            break

        }
      },
      //网络请求
      getHomeMultidata(){
        getHomeMultidata().then(res=>{
          // console.log(res);
          this.banners=res.data.banner.list;
          this.recommends=res.data.recommend.list;
        })
      },
      getHomedata(type){
        const page=this.goods[type].page+1;
        getHomedata(type,page).then(res=>{
          // console.log(res);
          this.goods[type].list.push(...res.data.list)

        })
        this.goods[type].page++;
      }
    }
  }
</script>

<style scoped>
  #home {
    padding-top: 44px;

  }
.home-nav {
  background-color: var(--color-tint);
  color:white;
  position: fixed;
  left: 0px;
  right: 0px;
  top: 0px;
  z-index: 9;
}
  .tabcontrol{
    position: sticky;
    top: 44px;
    z-index: 9;
  }
</style>
