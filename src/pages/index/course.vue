<template>
  <view class="course">
    <view class="indicator-wrap">
      <ul class="indicator" :style="{ '--active-index' : currentIndex}" @tap="tapChangeIndex">
        <li
          v-for="(item, index) in tabs"
          :data-index="index"
          :key="index"
          :class="currentIndex == index ? 'active' : ''"
        >
          {{ item }}
        </li>
      </ul>
    </view>
    <swiper :current="currentIndex" @change="swiperChangeIndex">
      <swiper-item>
        <view class="swiper-item my-class">
          <view class="my-class-card">
            <text>我的课程</text>
          </view>
        </view>
      </swiper-item>
      <swiper-item>
        <view class="swiper-item hot-courses">
          <view class="">
            <text>热门课程</text>
          </view>
        </view>
      </swiper-item>
      <swiper-item>
        <view class="swiper-item hot-courses">
          <view class="swiper-item">
            <text>选课指南</text>
          </view>
        </view>
      </swiper-item>
    </swiper>
  </view>
</template>

<script>
export default {
  data() {
    return {
      currentIndex: 0,
      tabs: ["我的课程", "热门课程", "选课指南"]
    };
  },
  onLoad() {},
  methods: {
    tapChangeIndex(e) {
      this.currentIndex = e.target.dataset.index;
    },
    swiperChangeIndex(e) {
      this.currentIndex = e.detail.current;
    }
  }
};
</script>

<style lang="stylus" scoped>
.indicator-wrap
	padding 20px 20px
	.indicator
		position relative
		display flex
		font-size 12px
		font-weight bold
		transition all .5s ease
		&::after
			position absolute
			content ""
			bottom -5px
			left 0
			transform translateX(calc(13px + 64px*var(--active-index)))
			transition .5s ease
			height 2px
			width 20px
			background-color #eb4559
		.active
			color #eb4559
		> li
			padding-right 15px
.my-class-card
	width 90vw
	height 200px
	margin 0 auto
	background-color #ffae8f
</style>
