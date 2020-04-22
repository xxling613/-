<template>
  <div class="my">
      <div class="user">
           <div v-if="show" class="user-defult">
               <!-- <open-data default-avatar></!--> 
              <img class="userImg" src="https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1586598727120&di=4f9d2d40dd7f682b80f5a3c447eb2636&imgtype=0&src=http%3A%2F%2Fimg.duoziwang.com%2F2017%2F09%2F1608485272991.jpg" alt="" >
              <p @click="toLogin">点击获取姓名</p>
           </div>
           <div v-if="!show" class="new-user">
               <!-- <img src="" alt=""> -->
              <div class="userImg" >
                 <open-data   type="userAvatarUrl" ></open-data>
              </div>
               <open-data type="userNickName"></open-data>
           </div>
      </div>
     <div class="operation ">
         <ul>
             <li>我的足迹 <span> > </span></li>
             <li>常见问题 <span> > </span></li>
             <li ><button open-type="contact">联系客服</button> <span> > </span></li>
             <li>关联公众号 <span> > </span></li>
         </ul>
     </div>
  </div>
</template>

<script>

export default {
   data(){
     return{
        show:true,
     }
   },
   onLoad(){
      this.getUserInfo()
      wx.showToast({
        title:'加载中',
        icon:'loading',
        duration:1000
      })
   },
   methods: {
      //授权获取用户信息
     getUserInfo(){
       var This=this;
        wx.getSetting({
          success (res){
            if (res.authSetting['scope.userInfo']) {
               This.show=false;
              // 已经授权，可以直接调用 getUserInfo 获取头像昵称
              wx.getUserInfo({
                success: function(res) {
                wx.switchTab({
                  url: '/pages/my/main',
                })
                 wx.hideToast()
                }
              })
            }
          }
          })
        },
        //跳转到登录页面
        toLogin(){
           wx.redirectTo({
                url: '/pages/login/main',
            })
        },
        //客服
        service(){

        }
   },
}
</script>

<style scoped>
  .my{
    background: white;
    width: 100%;
    height: 100vh;
    /* padding: 20px;
    box-sizing: border-box; */
  }
  .user{
    width: 100%;
    padding: 20px 0;
    text-align: center;
    background: #f75360;
    /* box-sizing: border-box; */
  }
  .userImg{
    width: 50px;
    height: 50px;
    border-radius: 50%;
    overflow: hidden;
    margin:0 auto;
  }
  .operation{
    margin: 10px 0;
    /* padding: 0 20px;
    box-sizing: border-box; */
  }
  .operation li{
    width: 100%;
    height: 40px;
    line-height: 40px;
    padding: 0 20px;
    border-bottom:1px solid gray;
    position: relative;
    font-size: 16px;
    box-sizing: border-box;
  }
  .operation span{
    position: absolute;
    right:20px;
    top:0;
  }
  .operation button{
    width: 100%;
    height: 100%;
    background: transparent;
    border:none;
    margin:0;
    padding:0;
    font-size:16px;
    text-align: left;
    position:static;
  }
</style>
