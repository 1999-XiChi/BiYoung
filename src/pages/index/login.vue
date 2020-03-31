<template>
  <view class="zaiui-login-content">
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
</template>

<script>
export default {
  data() {
    return {};
  },
  onLoad() {},
  methods: {
    tapBtn() {
      uni.navigateTo({
        url: "/pages/login/code"
      });
    },
    tapLogin() {
      uni.navigateTo({
        url: "/pages/login/login"
      });
    },
    signin() {
      wx.login({
        success(res) {
          console.log("用户的code:" + res.code);
        }
      });
    }
  }
};
</script>

<style>
@import "../../static/zaizai/login.css";
</style>
