<template>
    <div class="home">
        <div class="home-img">
          <img :src="homeList.imgs" alt="">
          <div class="explain">活 动 说 明</div>
        </div>
        <div class="home-explain">
            <h3 class="title">{{homeList.title}}</h3>
            <div class="countdown">
               <p>  离 投 票 倒 计 时 </p>
               <p>  {{5}} <span class="time">天</span>  
                    {{14}} <span class="time">时</span>  
                    {{22}} <span class="time">分</span>  
                    {{13}} <span class="time">秒</span> </p>
            </div>
        </div>
        <div class="home-data">
             <div class="data-item"> 
               <p>{{homeList.num}}</p>
               <p>已报名</p>
             </div>
             <div class="data-item"> 
               <p> {{homeList.ticket}} </p>
               <p>累计投票</p>
             </div>
             <div class="data-item"> 
               <p>{{homeList.visit}}</p>
               <p>访问量</p>
             </div>
        </div>
        <div class="search">
          <div>
             <input type="text" placeholder="请输入名称" v-model="name">
          </div>
          <div @click="search">搜索</div>
        </div>
        <div class="main">
            <ul class="main-title">
              <li :class="{active:navindex==1}" @click="getNewList(id)">最新</li>
              <li :class="{active:navindex==2}" @click="getHotList(id)">热门</li>
              <li :class="{active:navindex==3}" @click="getRankList(id)">排行榜</li>
            </ul>
            <div class="main-img">
              <div class="main-item" v-for="(item,index) in imgList"
               :key="index"
               @click="todetle(item.img,item.num,item.name,item.ticket)">
                   <img :src="item.img" alt="">   
                   <div class="num"> {{item.num}} </div>
                   <div class="name">
                      <ul>
                         <li> {{item.name}} </li>
                         <li> {{item.ticket}} </li>
                      </ul>
                   </div>
                   <p v-show="show">没有相关数据</p>
              </div>
            </div>
        </div>
        <button class="share" open-type="share"> 分享</button>
        <footer>
            <ul>
               <li>我要报名</li>
               <li>我的投票</li>
            </ul>
        </footer>
    </div>
</template>

<script>
import actives from '../../data/active'

export default {
    data(){
      return{
          id:"",
          homeList:{},
          activeList:[],
          navindex:1,
          imgList:[],
          navList:[
            {title:"最新",name:"new"},
            {title:"热门",name:"hot"},
            {title:"排行",name:"rank"}
          ],
          name:'',
          newList:[],
          show:false
      }
    },
    onLoad(options){
      this.id=options.pageId;
    },
    mounted() {
      this. getActiveList();
      this.getHomeList();
      this.getNewList(this.id);
    },
    onShareAppMessage: function(options) {
      return{
        title:this.homeList.title,
        imageUrl:this.homeList.img
      }
	 },
    methods: {
      //获取活动数据
      getActiveList(){
        this.activeList=actives.active.data;
      },
      //获取活动首页数据
      getHomeList(){
        this.activeList.map((item)=>{
          if(item.id==this.id){
            return this.homeList=item
          }
        })
      },
      //获取最新列表
      getNewList(id){
        this.navindex=1;
        this.imgList=actives.active.data[id-1].new;
        // console.log(actives.active.data[id-1].new)
      },
        //获取最火列表
      getHotList(id){
        this.navindex=2;
        this.imgList=actives.active.data[id-1].hot;
      },
        //获取排行榜列表
      getRankList(id){
        this.navindex=3;
        this.imgList=actives.active.data[id-1].rank;
      },
      //搜索
      search(){
        var name=this.name;
        var newList=[];
         if(name){
            this.imgList.map((item)=>{
           if(item.name.search(name)!=-1){
            newList.push(item)
           }
           return newList
         })
          this.imgList=newList;
         }
      },
      //跳转详情
      todetle(img,num,name,ticket){
        var url=`/pages/detail/main?detImg=${img}&&detNum=${num}&&detName=${name}&&detTicket=${ticket}`;
        wx.navigateTo({
          url:url
        })
    }
      // searchDefaule(e){
      //   var val=e.target.value;
      //   var searchList=[];
      //   var This=this;
      //   console.log(val)
      //   if(val){
      //     This.imgList.forEach((item)=>{
      //         if(item.name.indexOf(val)!=-1){
      //         searchList.push(item)
      //       }
      //         return searchList
      //       })
      //         This.imgList.splice(0);
      //         This.imgList.push(searchList)
      //         // console.log(searchList)
      //   }
      // }
    },
    // computed: {
    //   imgList(){
    //     if(this.name){
    //       return this.imgList.filter((value)=>{
    //         return value.includes(this.name)
    //         console.log(value.includes(this.name))
    //       })
    //     }
    //   }
    // },
  
}
</script>

<style  scoped>
  .home{
    background: white;
    margin-bottom: 50px;
  }
  .home-img{
    width: 100%;
    height: 200px;
    position: relative;
  }
  .home-img img{
    width: 100%;
    height: 100%;
  }
  .home-explain{
    padding: 20px 10px;
    text-align: center
  }
  .title{
    font-size: 18px;
    color:#ff90A3;
  }
  .countdown{
    width: 100%;
    padding: 10px;
    background: #f1f1f1;
    color: #ff90A3;
    margin-top:10px;
    box-sizing: border-box;
  }
  .time{
    color: gray;
    margin-right: 10px;
  }
  .explain{
    position: absolute;
    top:20%;
    right: 0;
    width: 100px;
    height: 30px;
    line-height: 30px;
    background: #f75360;
    border-top-left-radius:20px;
    border-bottom-left-radius:20px;
    text-align: center;
    color: white;
    font-size: 14px;
    border:1px solid white;
  }
  .countdown p{
    font-size: 16px;
  }
 .countdown p:first-child{
   margin-bottom: 10px
 }
 .home-data{
   display: flex;
   justify-content: center
 }
 .data-item{
   flex: 1;
   padding: 10px;
   text-align: center;
 }
 .data-item p:first-child{
    color: #ff90A3;
    font-size: 18px;
    margin-bottom: 10px;
 }
 .data-item p:last-child{
    color: gray;
    font-size: 12px
 }
 .search{
   display: flex;
   justify-content: center;
   padding: 10px;
   font-size: 16px;
   height: 40px;
   line-height: 40px;
 }
 .search div{
   border: 1px solid #f75360;
   border-radius: 20px;
 }
 .search div:first-child{
   flex:4;
 }
  .search input{
    width: 100%;
    height: 100%;
    padding:0 20px;
    box-sizing: border-box;
  }
 .search div:last-child{
   flex: 1;
   margin-left: 10px;
   text-align: center;
   color: #f75360;
 }
 .main-title{
   display: flex;
   justify-content: center;
   align-items: center;
   padding:15px 0;
 }
 .main-title li{
   flex: 1;
   font-size: 16px;
   text-align: center
 }
 .defult{
   color: gray;
 }
 .active{
    color: #f75360;
 }
 .main-img{
   padding: 10px;
   display: flex;
   flex-wrap: wrap;
   justify-content: space-between;
 }
 .main-item{
   width: 48%;
   display: flex;
   flex-direction: column;
   justify-content: space-between;
   margin-bottom: 10px;
   border-radius: 15px;
   box-shadow: 1rpx 1rpx 10rpx 3rpx gray;
   position: relative;
 }
 .main-item img{
   width:100%;
   height: 140px;
   border-radius: 15px;
   /* margin:auto; */
   /* flex-grow: 1;
   object-fit: cover */
   }
   .num{
     position: absolute;
     top:0;
     right:0;
     width: 40px;
     height: 30px;
     line-height: 30px;
     background: rgba(0,0,0,0.4);
     border-bottom-left-radius: 100%;
     z-index:10;
     border-top-right-radius: 15px;
     color: white;
     font-size: 15px;
     text-align: center;
   }
   .name{
     position: absolute;
     left: 0;
     bottom: 0;
     width: 100%;
     height:20px;
     color: white;
     text-align: center;
     font-size: 14px;
     overflow: hidden;
   }
   .name li:first-child{
     position: absolute;
     left:20px;
     top:0;
     white-space: nowrap;
     overflow: hidden;
     text-overflow: ellipsis;
   }
   .name li:last-child{
     position: absolute;
     right:20px;
     top:0;
   }
   .share{
     position: fixed;
     right:20px;
     bottom:70px;
     background: #f75360;
     color: white;
     /* width: 60px; */
     height: 60px;
     line-height: 60px;
     border-radius: 50%;
     text-align: center;
     font-size: 15px;
   }
   footer{
     width: 100%;
     height: 60px;
     position: fixed;
     left: 0;
     bottom:0;
     padding: 10px;
     background: white;
     z-index: 99;
     overflow: hidden;
     box-sizing: border-box;
     text-align: center
     /* display: flex;
     justify-content: center;
     align-items: center */
   }
  footer li:first-child{
    float: left;
    width: 48%;
    height: 38px;
    line-height: 38px;
    border-radius: 15px;
    border: 1px solid #f75360;
    color: #f75360
  }
  footer li:last-child{
    float:right;
    width: 48%;
    height: 38px;
    line-height: 38px;
    border-radius: 15px;
    background: #f75360;
    color: white
  }
</style>
