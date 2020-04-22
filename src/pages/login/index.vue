<template>
  <div class="login">
      <p>申请获取以下权限</p>
      <p>获得你的公开信息(昵称，头像等)</p>
      <button open-type="getUserInfo"  @getuserinfo="getUserInfo">授权登录</button> 
  </div>
</template>

<script>

export default {
   data(){
     return{

     }
   },
   methods: {
     getUserInfo(){
       let This=this;
       // 查看是否授权
      wx.getSetting({
        success (res){
          if (res.authSetting['scope.userInfo']) {
            // 已经授权，可以直接调用 getUserInfo 获取头像昵称
            wx.getUserInfo({
              success: function(res) {
                console.log(res)
                wx.reLaunch({
                url: '/pages/my/main',
              })
              }
            })
          }
          // else{
          //           wx.showModal({
          //           title: '提示',
          //           content: '需要授权才能进入，是否授权?',
          //           success (res) {
          //             if (res.confirm) {
          //               console.log('用户点击确定')
          //               wx.redirectTo({
          //               url: '/pages/my/main',
          //           })
          //             } else if (res.cancel) {
          //               console.log('用户点击取消')
          //             }
          //           }
          //         })
          // }
        }
      })
     }
   },
}
</script>

<style scoped>
   .login{
     width: 100%;
     height: 100vh;
     padding: 20px 10px;
     color:#f75360;
     background: white;
     box-sizing: border-box;
   }
   button{
     width: 100%;
     height: 40px;
     line-height: 40px;
     background: #f75360;
     color: white;
     border-radius:20px;
     margin: 50px 0;
   }
</style>
