<template>
  <view class="index">
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
    <swiper
      :style="{ height: clientHeight ? clientHeight + 'px' : 'auto' }"
      class="swiper"
      :current="currentIndex"
      @change="swiperChangeIndex"
    >
      <swiper-item>
        <scroll-view
          scroll-y="true"
          :style="{ height: clientHeight ? clientHeight + 'px' : 'auto' }"
        >
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
                    v-for="(course, i) in sortingCourses"
                    :key="i"
                  >
                    <view
                      class="sortingCourse-icon-bg"
                      :style="{ backgroundColor: course.color }"
                    >
                      <img class="sortingCourse-icon" :src="course.icon" />
                    </view>
                    <text class="sortingCourse-text">{{ course.text }}</text>
                  </li>
                </ul>
              </scroll-view>
            </view>
            <view class="courses-wrap">
              <view class="head">
                <text class="title">在线微课</text>
                <text class="subtitle">快来试听吧~</text>
                <view class="subjects" @tap="changeSubject">
                  <view
                    :class="[
                      'subject',
                      currentSubjectIndex === i ? 'active' : ''
                    ]"
                    :data-index="i"
                    v-for="(subject, i) in subjects"
                    :key="i"
                    >{{ subject }}</view
                  >
                </view>
              </view>
              <view class="contain">
                <view
                  class="course-card"
                  v-for="(course, i) in courseCards"
                  :key="i"
                >
                  <view class="head">
                    <view class="title">
                      <view class="subject">{{ course.subject }}</view>
                      <view class="name">{{ course.name }}</view>
                    </view>
                    <view class="detail">
                      <view class="time">{{ course.time }} · </view>
                      <view class="grade"> {{ course.grade }}</view>
                    </view>
                  </view>
                  <view class="footer">
                    <view class="teachers">
                      <view
                        v-for="(teacher, i) in course.teachers"
                        :key="i"
                        class="teacher"
                      >
                        <img
                          src="http://biyoung.xichi.xyz/icon/avatar_boy.png"
                          class="avatar"
                        />
                        <text>{{ teacher }}</text>
                      </view>
                    </view>
                    <view class="right">
                      <view class="cost">￥ {{ course.cost }}</view>
                      <view class="count">{{ course.count }}人已经报名</view>
                    </view>
                  </view>
                </view>
              </view>
            </view>
          </view>
        </scroll-view>
      </swiper-item>
      <swiper-item>
        <scroll-view
          scroll-y="true"
          :style="{ height: clientHeight ? clientHeight + 'px' : 'auto' }"
        >
          <view class="growth-example index-item">
            <text>成长榜样</text>
          </view>
        </scroll-view>
      </swiper-item>
      <swiper-item>
        <scroll-view
          scroll-y="true"
          :style="{ height: clientHeight ? clientHeight + 'px' : 'auto' }"
        >
          <view class="about-us index-item">
            <text>关于BiYoung</text>
          </view>
        </scroll-view>
      </swiper-item>
    </swiper>
  </view>
</template>

<script>
export default {
  data() {
    return {
      currentIndex: 0,
      tabs: ["热门课程", "成长榜样", "关于我们"],
      myCourses: [],
      studyTime: "0分钟",
      hotCourses: [
        "http://biyoung.xichi.xyz/courses/banner/1a6eef83cc835d092fe97ac0cd727ed0.jpg",
        "http://biyoung.xichi.xyz/courses/banner/0e436fc5cae53f0a0332458f91cd597c.png",
        "http://biyoung.xichi.xyz/courses/banner/92d8e63f6c5dadb3cf1885766d6e6b34.png",
        "http://biyoung.xichi.xyz/courses/banner/aeafb46398a160cac13f63440aa0bcf7.jpg"
      ],
      sortingCourses: [
        {
          icon:
            "http://biyoung.xichi.xyz/course/icon/%E8%AF%BE%E7%A8%8B%E8%A1%A5%E6%97%B6.svg",
          text: "限时免费",
          color: "#eb4559"
        },
        {
          icon:
            "http://biyoung.xichi.xyz/course/icon/%E8%AF%BE%E7%A8%8B%20%281%29.png",
          text: "期末复习",
          color: "#084177"
        },
        {
          icon:
            "http://biyoung.xichi.xyz/course/icon/%E8%AF%BE%E7%A8%8B%E8%A1%A8.png",
          text: "高分策略",
          color: "#ffae8f"
        },
        {
          icon:
            "http://biyoung.xichi.xyz/course/icon/%E8%AF%BE%E7%A8%8B%20%282%29.png",
          text: "名师专栏",
          color: "#fddb3a"
        },
        {
          icon: "http://biyoung.xichi.xyz/course/icon/%E8%AF%BE%E7%A8%8B.png",
          text: "兴趣开发",
          color: "#1eb2a6"
        },
        {
          icon:
            "http://biyoung.xichi.xyz/course/icon/%E8%AF%BE%E7%A8%8B%E5%BD%A2%E5%BC%8F.png",
          text: "演讲口才",
          color: "#b590ca"
        },
        {
          icon:
            "http://biyoung.xichi.xyz/course/icon/%E8%AF%BE%E7%A8%8B%E6%9F%A5%E8%AF%A2.png",
          text: "作文补习",
          color: "#f6d186"
        },
        {
          icon:
            "http://biyoung.xichi.xyz/course/icon/%E8%AF%BE%E7%A8%8B%E7%94%BB%E5%83%8F.png",
          text: "英语集训",
          color: "#00a8cc"
        }
      ],
      subjects: ["热门", "语文", "数学", "英语", "科学", "兴趣"],
      currentSubjectIndex: 0,
      courseCards: [
        {
          name: "编程思维训练班",
          teachers: ["王坤", "胡里山"],
          subject: "兴趣",
          time: "4.23-9.19",
          grade: "小学六年级",
          cost: "99",
          count: "66"
        },
        {
          name: "名家写作班",
          teachers: ["闻喜想"],
          subject: "语文",
          time: "4.23-5.19",
          grade: "小学六年级",
          cost: "199",
          count: "36"
        },
        {
          name: "英语演讲班",
          teachers: ["徐旭才"],
          subject: "英语",
          time: "5.23-3.19",
          grade: "小学六年级",
          cost: "599",
          count: "35"
        },
        {
          name: "编程思维训练班",
          teachers: ["王坤", "胡里山"],
          subject: "兴趣",
          time: "4.23-9.19",
          grade: "小学六年级",
          cost: "99",
          count: "66"
        }
      ],
      clientHeight: 0
    };
  },
  onLoad() {
    this.getClientHeight();
  },
  methods: {
    tapChangeIndex(e) {
      this.currentIndex = e.target.dataset.index;
    },
    swiperChangeIndex(e) {
      this.currentIndex = e.detail.current;
    },
    changeSubject(e) {
      this.currentSubjectIndex = e.target.dataset.index;
    },
    getClientHeight() {
      var that = this;
      uni.getSystemInfo({
        success: function(res) {
          that.clientHeight = res.windowHeight;
        }
      });
    }
  }
};
</script>

<style lang="stylus" scoped>
redColor = #eb4559
.index
  background-color #FDFDFD
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
        background-color redColor
      .active
        color redColor
      > li
        padding-right 15px
  .swiper
    .index-item
      padding 0 5vw
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
        margin 0 0 10px 0
        padding 10px 0
        box-shadow 0 0 15px 0 #E5EAF0
        .scroll-view-item_H
          display inline-block
          width 93%
          .sortingCourse
            display inline-block
            width 20%
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
        margin-top 5px
        padding 0 5vw
        box-shadow 0 0 5px 0 #E5EAF0
        .head
          .title
            font-size 14px
            font-weight bold
            letter-spacing .1em
          .subtitle
            font-size 12px
            color #999
            padding-left 5px
          .subjects
            display flex
            margin-top 2px
            .subject
              margin 3px 5px
              padding 3px 8px
              font-size 10px
              border 1px solid #666
              border-radius 12px
              color #666
              &:first-child
                margin-left -1px
            .active
              background-color redColor
              color #ffffff
              border none
        .contain
          padding-bottom 20px
          .course-card
            width 100%
            height 100px
            margin 10px auto
            padding 10px 5px
            box-shadow 0 0 10px 0 #E5EAF0
            border-radius 5px
            display flex
            flex-direction column
            justify-content space-between
            .title, .detail, .footer
              display flex
            .head
              .title
                display flex
                align-items center
                .subject
                  background-color #f9a825
                  font-weight 400
                  font-size 12px
                  line-height 15px
                  height 15px
                  padding 0 2px
                  color #fff
                .name
                  margin-left 5px
              .detail
                font-size 13px
                color #666
            .footer
              display flex
              justify-content space-between
              padding 0 5px
              .teachers
                display flex
                .teacher
                  display flex
                  flex-direction column
                  font-size 12px
                  color #333
                  margin-right 10px
                  .avatar
                    width 50rpx
                    height 50rpx
              .right
                display flex
                flex-direction column
                justify-content space-around
                .cost
                  color #ff5252
                  font-size 13px
                  font-weight bold
                .count
                  color #666
                  font-size 11px
    .curse-selection-guide
      height 1600px
</style>
