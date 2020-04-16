<template>
  <view class="login">
    <view class="zaiui-login-content" v-if="!Login">
      <view class="logo-view">
        <image class="logo" src="/static/logo.png" mode="widthFix"></image>
      </view>
      <view class="content">
        <view class="title-h">您好,</view>
        <view class="introduce">欢迎使用BiYoung~</view>
        <input class="phone-input" placeholder="请输入手机号码" />
      </view>
      <view class="foot-view">
        <view class="zaiui-btn-view">
          <button class="zaiui-btn" @tap="tapBtn">获取验证码</button>
        </view>
        <view class="font-tag-view">
          <text class="font-tag" @tap="tapLogin">密码登录</text>
          <text class="font-tag" @tap="signin">微信登录</text>
        </view>
      </view>
    </view>
    <view class="profile" v-else>
      <view class="center">
        <view class="center_top">
          <view class="mask"></view>
        </view>
        <view class="center_box_bg">
          <view class="profily">
            <view class="base">
              <view
                class="profily_header"
                :style="'background-image:url(' + userInfo.avatar + ')'"
              >
              </view>
              <text>{{ userInfo.name }}</text>
              <image
                src="../../static/fumou-center-template/setting.png"
                mode=""
              ></image>
            </view>
            <view class="order_status">
              <view class="status" v-for="(item, i) in status" :key="i">
                <image class="icon" :src="item.url" mode="aspectFill"></image>
                <text>{{ item.name }}</text>
              </view>
            </view>
          </view>
          <view class="baiban"> </view>
          <view class="center_menu">
            <view class="menu_item" v-for="(item, i) in menus" :key="i">
              <image :src="item.icon" mode="aspectFill"></image>
              <text>{{ item.name }}</text>
            </view>
          </view>
        </view>
      </view>
      <view class="signOutBtn">
        <text @tap="signOut">退出登录</text>
      </view>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      Login: false,
      userInfo: {
        name: "小Young",
        avatar: "http://biyoung.xichi.xyz/avatar/avatar3.jpg",
      },
      status: [
        {
          key: 1,
          name: "我的班级",
          url: "../../static/fumou-center-template/one.png",
        },
        {
          key: 2,
          name: "学习轨迹",
          url: "../../static/fumou-center-template/2.png",
        },
        {
          key: 3,
          name: "我的荣誉",
          url: "../../static/fumou-center-template/3.png",
        },
        {
          key: 4,
          name: "我的心情",
          url: "../../static/fumou-center-template/4.png",
        },
      ],
      menus: [
        {
          name: "我的收藏",
          icon: "../../static/fumou-center-template/5.png",
          key: 1,
        },
        {
          name: "消息管理",
          icon: "../../static/fumou-center-template/6.png",
          key: 2,
        },
        {
          name: "综合评价",
          icon: "../../static/fumou-center-template/7.png",
          key: 3,
        },
        {
          name: "帮助中心",
          icon: "../../static/fumou-center-template/8.png",
          key: 4,
        },
        {
          name: "意见反馈",
          icon: "../../static/fumou-center-template/9.png",
          key: 5,
        },
        {
          name: "关于我们",
          icon: "../../static/fumou-center-template/10.png",
          key: 6,
        },
      ],
    };
  },
  onLoad() {},
  methods: {
    tapBtn() {
      uni.navigateTo({
        url: "/pages/login/code",
      });
    },
    tapLogin() {
      uni.navigateTo({
        url: "/pages/login/login",
      });
    },
    signin() {
      this.Login = true;
      wx.login({
        success(res) {
          console.log("用户的code:" + res.code);
        },
      });
    },
    signOut(){
      this.Login = false;
    }
  },
};
</script>

<style lang="stylus" scoped>
@import "../../static/zaizai/login.css";
@import "../../static/fumou-center-template/profile.css"
.profile
  width 100vw
  height 100vh
  .signOutBtn
    border-radius 30px
    text-align center
    width 250px
    height 30px
    line-height 30px
    margin 0 auto
    margin-bottom 30px
    color #ffffff
    background-color #F56C6C
</style>
