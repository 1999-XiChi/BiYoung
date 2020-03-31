<template>
  <view class="zaiui-login-content">
    <view class="logo-view">
      <image class="logo" src="/static/logo.jpg" mode="widthFix"></image>
    </view>
    <view class="content">
      <view class="title-h">验证</view>
      <view class="introduce">
        <text class="tap" @tap="checking" v-if="!state">重新获取验证码</text>
        <text v-else>{{ currentTime }}s 后可重新获取验证码</text>
      </view>
      <view class="zaiui-flex-view checking-view">
        <view class="flex-sub text-center">
          <input class="phone-input" type="number" maxlength="1" />
        </view>
        <view class="flex-sub text-center">
          <input class="phone-input" type="number" maxlength="1" />
        </view>
        <view class="flex-sub text-center">
          <input class="phone-input" type="number" maxlength="1" />
        </view>
        <view class="flex-sub text-center">
          <input class="phone-input" type="number" maxlength="1" />
        </view>
        <view class="flex-sub text-center">
          <input class="phone-input" type="number" maxlength="1" />
        </view>
        <view class="flex-sub text-center">
          <input class="phone-input" type="number" maxlength="1" />
        </view>
      </view>
      <view class="right-tip-view">
        <text>收不到验证码？</text>
        <text class="tap">使用语音验证</text>
      </view>
    </view>
    <view class="foot-view">
      <view class="zaiui-btn-view">
        <button class="zaiui-btn" @tap="signin">登录</button>
      </view>
      <view class="font-tag-view">
        <text class="font-tag" @tap="tapLogin">密码登录</text>
        <text class="font-tag">微信登录</text>
      </view>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      state: false, //是否开启倒计时
      totalTime: 120, //总时间，单位秒
      recordingTime: 0, //记录时间变量
      currentTime: 0 //显示时间变量
    };
  },
  onLoad() {
    //this.checking();
  },
  methods: {
    checking() {
      //把显示时间设为总时间
      this.currentTime = this.totalTime;
      //开始倒计时
      this.state = true;
      //执行倒计时
      this.checkingTime();
    },
    checkingTime() {
      let that = this;
      //判断是否开启
      if (this.state) {
        //判断显示时间是否已到0，判断记录时间是否已到总时间
        if (this.currentTime > 0 && this.recordingTime <= this.totalTime) {
          //记录时间增加 1
          this.recordingTime = this.recordingTime + 1;
          //显示时间，用总时间 - 记录时间
          this.currentTime = this.totalTime - this.recordingTime;
          //1秒钟后，再次执行本方法
          setTimeout(() => {
            //定时器内，this指向外部，找不到vue的方法，所以，需要用that变量。
            that.checkingTime();
          }, 1000);
        } else {
          //时间已完成，还原相关变量
          this.state = false; //关闭倒计时
          this.recordingTime = 0; //记录时间为0
          this.currentTime = this.totalTime; //显示时间为总时间
        }
      } else {
        //倒计时未开启，初始化默认变量
        this.state = false;
        this.recordingTime = 0;
        this.currentTime = this.totalTime;
      }
    },
    tapLogin() {
      uni.navigateTo({
        url: "/pages/login/login"
      });
    }
  }
};
</script>

<style>
@import "../../static/zaizai/login.css";
</style>
