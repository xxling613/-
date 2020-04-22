<template>
  <div class="active">
     <div class="active-list">
         <ul>
            <li v-for="(item,index) in activeList" :key="index" @click="toActivePage(item.id)">
               <div class="active-img">
                  <img :src="item.imgs" alt="">
               </div>
               <div class="active-intro">
                  <h3>{{item.title}}</h3>
                  <p class="active-num">{{item.num}}人参与,已投{{ticket}}票</p>
                  <p class="active-time">{{item.countdown.endtime}} 结束</p>
               </div>
            </li>
         </ul>
     </div>
  </div>
</template>

<script>
import actives from '../../data/active'

export default {                             
   data(){
     return{
       activeList:[]
     }
   },
   mounted() {
    this.getActiveList();
   },
   methods: {
     //获取数据
     getActiveList(){
        this.activeList=actives.active.data;
     },
     //路由跳转
    toActivePage(id){
      var url='/pages/page/main?pageId='+id;
      wx.navigateTo({url})
    }
   },
}
</script>

<style scoped>
  .active{
    padding: 20px;
    background: #ff90A3
  }
  .active-list li{
    width:100%;
    /* height: 400px; */
    background: white;
    font-size: 16px;
    margin-bottom: 10px;
    border-radius: 10px
  }
  .active-img{
    width: 100%;
    height: 230px;
  }
  .active-img img{
    width: 100%;
    height: 100%;
    border-top-left-radius: 10px;
    border-top-right-radius: 10px;
  }
  .active-intro{
    padding: 10px
  }
  .active-intro h3{
   font-size: 18px;
   white-space: nowrap;
   overflow: hidden;
   text-overflow: ellipsis
  }
  .active-num{
   margin: 10px 0
  }
  .active-time{
    font-size: 12px;
    color: gray
  }
</style>
