<template>
	<view class="zaiui-login-content">
		<view class="logo-view">
			<image class="logo" src="/static/logo.png" mode="widthFix"></image>
		</view>
		<view class="content">
			<view class="title-h">您好,</view>
			<view class="introduce">欢迎使用BiYoung~</view>
			<input class="phone-input" placeholder="请输入手机号码"/>
			<input class="phone-input" password placeholder="请输入登录密码"/>
		</view>
		<view class="foot-view">
			<view class="zaiui-btn-view">
				<button class="zaiui-btn">登录</button>
			</view>
			<view class="font-tag-view">
				<text class="font-tag" @tap="tapLogin">免密码登录</text>
				<text class="font-tag">微信登录</text>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		onLoad() {

		},
		methods: {
			tapLogin() {
				uni.navigateTo({
					url: '/pages/login/index'
				});
			}
		}
	}
</script>

<style>
	@import '../../static/zaizai/login.css';
	
</style>
