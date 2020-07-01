<template>
  <div class="headportrait">
    <img class="index_img" :src="getUserlist.avatarUrl" alt />
    <div class="Study">
      <!-- <p @tap="toDetail">进入新大陆</p> -->
      <p class="userName">{{ getUserlist.nickName }}</p>
      <!-- getuserinfo响应数据保存，open-type启动获取权限 -->
      <van-button
        v-if="isShow"
        plain
        round
        color="#333333"
        icon="manager"
        open-type="getUserInfo"
        @getuserinfo="getUserInfo"
      >点击获取账号信息</van-button>
      <van-button
        v-else
        plain
        round
        color="#333333"
        open-type="getUserInfo"
        @getuserinfo="getUserInfo"
        @tap="toDetail"
      >进入新大陆</van-button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      // 用户信息保存
      getUserlist: {},
      isShow: true
    };
  },
  // 这个生命周期最好，适合获取微信API登陆
  beforeMount() {},
  mounted() {},
  // 这里主要是用于vue加载
  methods: {
    getUserInfo() {
      // 定义this
      let that = this;
      wx.getUserInfo({
        success: function(res) {
          // 获取数据 （在微信小程序里面不可以直接获取用户信息，需要请求对方同意才可以）
          that.getUserlist = res.userInfo;
          that.isShow = false;
        },
        fail: res => {
          console.log("获取失败");
        }
      });
    },
    toDetail() {
      wx.navigateTo({
        // 进入页面
        url: "/pages/list/main"
      });
    }
  }
};
</script>

<style>
page {
  background: #333333;
}
text2 {
  text-align: center;
  width: 80%;
}
.headportrait {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.index_img {
  width: 200px;
  height: 200px;
  border-radius: 240rpx;
  margin: 100rpx 0%;
}
.userName {
  text-align: center;
  font-size: 40rpx;
  font-weight: bold;
  margin: 100rpx 0;
  color: aqua;
}
</style>
