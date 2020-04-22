<template>
  <div class="detail">
    <div class="introduce">
      <h2>{{detList.detNum}}号选手  {{detList.detName}}</h2>
        <p>正在参加，快来参赛</p>
     </div> 
    <div class="home-data">
             <div class="data-item"> 
               <p>{{detList.detNum}}</p>
               <p>编号</p>
             </div>
             <div class="data-item"> 
               <p> {{detList.detTicket}} </p>
               <p>票数</p>
             </div>
             <div class="data-item"> 
               <p>12</p>
               <p>排行</p>
             </div>
        </div>
        <div class="main">
            <img src="https://ss1.bdstatic.com/70cFuXSh_Q1YnxGkpoWK1HF6hhy/it/u=3902295990,2421687003&fm=26&gp=0.jpg" alt="">
            <h4>参赛介绍</h4>
            <p>{{detList.detName}}</p>
            <h4>热门选手</h4>
        </div>
        <footer>
            <div class="transmit" @tap="transmit">转发</div>
            <div class="vote">给TA投票</div>
            <div class="transmit">排行</div>
        </footer>
  </div>
</template>

<script>
import actives from '../../data/active'

export default {
     data(){
       return{
         detList:{}
       }
     },
     onLoad(options){
      this.detList=options
      console.log(options)
     },
    mounted() {
     
    }, 
    methods: {
      transmit(){
        // wx.showShareMenu({
        //   withShareTicket: true
        // })
      }
}
}
</script>

<style scoped>
   .detail{
      padding: 20px;
      box-sizing: border-box;
      background: white;
      text-align: center;
      padding-bottom: 50px;
   }
   .detail .introduce h2{
     color: #f75360;
     font-size: 20px;
   }
   .introduce p{
     margin: 10px 0;
     font-size: 15px;
     color: gray;
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
 .main img{
   width: 100%;
 }
 .main h4{
   margin: 20px 0;
   color:  #ff90A3;
   font-size:16px;
 }
 footer{
   width: 100%;
   height: 50px;
   line-height: 50px;
   position: fixed;
   left: 0;
   bottom: 10px;
   display: flex;
   justify-content: center;
   text-align: center;
   padding: 0 10px;
   box-sizing: border-box;
 }
 footer .transmit{
   flex: 1;
   background: #f75360;
   color: white;
   border-radius: 50%;
 }
 footer .vote{
   flex: 3;
   border-radius: 20px;
    background: #f75360;
   color: white;
   margin: 0 20px;
 }
</style>
