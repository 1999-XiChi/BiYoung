<template>
  <view class="course">
    <view class="indicator-wrap">
      <ul
        class="indicator"
        :style="{ '--active-index': currentIndex }"
        @tap="tapChangeIndex"
      >
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
    <swiper class="swiper" :current="currentIndex" @change="swiperChangeIndex">
      <swiper-item>
        <view class="swiper-item my-class">
          <view class="my-class-card">
            <text>我的课程</text>
          </view>
        </view>
      </swiper-item>
      <swiper-item>
        <view class="swiper-item hot-courses">
          <swiper indicator-dots autoplay class="banner-wrap">
            <swiper-item
              v-for="(item, index) in hotCourses"
              :key="index"
              class="banner"
            >
              <view
                class="banner-bg"
                :style="{ backgroundImage: `url(${item})` }"
              ></view>
            </swiper-item>
          </swiper>
          <view>
            <scroll-view class="scroll-view_H" scroll-x="true">
              <ul class="scroll-view-item_H">
                <li
                  class="sortingCourse"
                  v-for="(course, i) in sortingCourses1"
                  :key="i"
                >
                  <view class="sortingCourse-icon-bg" :style="{ backgroundColor: course.color}">
                    <img class="sortingCourse-icon" :src="course.icon" />
                  </view>
                  <text class="sortingCourse-text">{{ course.text }}</text>
                </li>
              </ul>
              <ul class="scroll-view-item_H">
                <li
                  class="sortingCourse"
                  v-for="(course, i) in sortingCourses2"
                  :key="i"
                >
                  <view class="sortingCourse-icon-bg" :style="{ backgroundColor: course.color }">
                    <img class="sortingCourse-icon" :src="course.icon" />
                  </view>
                  <text class="sortingCourse-text">{{ course.text }}</text>
                </li>
              </ul>
            </scroll-view>
          </view>
          <view class="courses-wrap">
            <view class="head">
              <text>在线微课<span>快来试听吧</span></text>
              <view class="subjects">
                <view v-for="subject in subjects">{{subject}}</view>
              </view>
            </view>
            <view class="contain">
              <view v-for="courseCard in courseCards"></view>
            </view>
          </view>
        </view>
      </swiper-item>
      <swiper-item>
        <view class="swiper-item curse-selection-guide">
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
      tabs: ["我的课程", "热门课程", "选课指南"],
      hotCourses: [
        "http://biyoung.xichi.xyz/courses/banner/1a6eef83cc835d092fe97ac0cd727ed0.jpg",
        "http://biyoung.xichi.xyz/courses/banner/0e436fc5cae53f0a0332458f91cd597c.png",
        "http://biyoung.xichi.xyz/courses/banner/92d8e63f6c5dadb3cf1885766d6e6b34.png",
        "http://biyoung.xichi.xyz/courses/banner/aeafb46398a160cac13f63440aa0bcf7.jpg"
      ],
      sortingCourses1: [
        {
          icon:
            "http://biyoung.xichi.xyz/course/icon/%E8%AF%BE%E7%A8%8B%E8%A1%A5%E6%97%B6.svg",
          text: "限时免费",
          color: "#eb4559"
        },
        {
          icon: "http://biyoung.xichi.xyz/course/icon/%E8%AF%BE%E7%A8%8B%20%281%29.png",
          text: "期末复习",
          color: "#084177"
        },
        {
          icon: "http://biyoung.xichi.xyz/course/icon/%E8%AF%BE%E7%A8%8B%20%282%29.png",
          text: "名师专栏",
          color: "#fddb3a"
        },
        {
          icon: "http://biyoung.xichi.xyz/course/icon/%E8%AF%BE%E7%A8%8B.png",
          text: "兴趣开发",
          color: "#1eb2a6"
        }
      ],
      sortingCourses2: [
        {
          icon: "http://biyoung.xichi.xyz/course/icon/%E8%AF%BE%E7%A8%8B%E5%BD%A2%E5%BC%8F.png",
          text: "演讲口才",
          color: "#b590ca"
        },
        {
          icon: "http://biyoung.xichi.xyz/course/icon/%E8%AF%BE%E7%A8%8B%E6%9F%A5%E8%AF%A2.png",
          text: "作文补习",
          color: "#f6d186"
        },
        {
          icon: "http://biyoung.xichi.xyz/course/icon/%E8%AF%BE%E7%A8%8B%E7%94%BB%E5%83%8F.png",
          text: "英语集训",
          color: "#00a8cc"
        },
        {
          icon: "http://biyoung.xichi.xyz/course/icon/%E8%AF%BE%E7%A8%8B%E8%A1%A8.png",
          text: "高分策略",
          color: "#678a74"
        }
      ],
      subjects: ["热门","语文","数学","英语","科学","其他"],
      courseCards: [{
        name: "编程思维训练班",
        teacher: "王坤",
        subject: "兴趣",
        time: "4.23-9.19",
        grade: "小学六年级",
        cost: "199",
        count: "66"
      }]
    };
  },
  onLoad() {},
  methods: {
    tapChangeIndex(e) {
      this.currentIndex = e.target.dataset.index;
    },
    swiperChangeIndex(e) {
      this.currentIndex = e.detail.current;
    },
    scroll(e) {
      console.log(e);
      this.old.scrollTop = e.detail.scrollTop;
    }
  }
};
</script>

<style lang="stylus" scoped>
.course
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
  .swiper
    min-height calc(100vh - 56px)
    .my-class-card
      width 90vw
      height 150px
      margin 0 auto
      background-color #ffae8f
    .hot-courses
      .banner-wrap
        width 100vw
        height 150px
        margin 0 auto
        .banner
          .banner-bg
            margin 0 auto
            width 90%
            height 150px
            background-position top
            background-size 150% 100%
      .scroll-view_H
        white-space nowrap
        margin 30rpx 0
        .scroll-view-item_H
          display inline-block
          width 90%
          .sortingCourse
            display inline-block
            width 25%
            .sortingCourse-icon-bg
              position relative
              width 60rpx
              height 60rpx
              border-radius 50%
              margin 0 auto
              .sortingCourse-icon
                position absolute
                width 40rpx
                height 40rpx
                top 50%
                left 50%
                transform translate(-50%, -50%)
            .sortingCourse-text
              display block
              text-align center
              font-size 12px
              line-height 40rpx
              color #666
      .courses-wrap
        .subjects
          display flex
    .curse-selection-guide
      height 1600px
</style>
