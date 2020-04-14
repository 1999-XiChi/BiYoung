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
          <view class="swiper-item my-class course-item-0">
            <view class="study-time-card">
              <view class="study-time-wrap"></view>
              <view class="study-time-main">
                <cmd-circle
                  cid="circle10"
                  type="circle"
                  :percent="studyTimeProgress"
                  :showInfo="false"
                  width="130"
                ></cmd-circle>
                <text class="info"
                  >{{ studyTime }}分钟 / {{ planTime }}分钟</text
                >
              </view>
              <view class="study-time-footer"
                >今日已学习：{{ studyTime }}分钟</view
              >
            </view>
            <view class="my-courses">
              <view class="head">
                <view>我的课程({{ myCourses.length }})</view>
                <view>全部 ∨</view>
              </view>
              <view class="contain">
                <view
                  class="course-card"
                  v-for="(course, i) in myCourses"
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
                      <view class="progress"
                        >已学<span class="number">{{
                          course.progress
                        }}</span></view
                      >
                      <view class="count">
                        <span style="font-weight:bold;padding-right: 3px;">{{
                          course.count
                        }}</span>
                        成员</view
                      >
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
          <view class="study-plan course-item-1">
            <imt-calendar :selected="calendarDate"></imt-calendar>
            <view class="study-task-wrap">
              <view class="title">课程</view>
              <view
                class="study-task"
                v-for="(task, index) in studyTasks"
                :key="index"
              >
                <text>{{ task.time }} {{ task.course }} {{ task.task }}</text>
                <text
                  class="status"
                  :style="{ color: statusColor(task.status) }"
                  >{{ task.status }}</text
                >
              </view>
            </view>
          </view>
        </scroll-view>
      </swiper-item>
    </swiper>
  </view>
</template>

<script>
import cmdCircle from "@/components/cmd-circle/cmd-circle.vue";
import imtCalendar from "components/imt-calendar/imt-calendar";
export default {
  components: { cmdCircle, imtCalendar },
  data() {
    return {
      currentIndex: 0,
      tabs: ["我的课程", "学习计划"],
      studyTime: 28,
      planTime: 60,
      clientHeight: 0,
      myCourses: [
        {
          name: "编程思维训练班",
          teachers: ["王坤", "胡里山"],
          subject: "兴趣",
          time: "4.23-9.19",
          grade: "小学六年级",
          progress: "33%",
          count: "66"
        },
        {
          name: "名家写作班",
          teachers: ["闻喜想"],
          subject: "语文",
          time: "4.23-5.19",
          grade: "小学六年级",
          progress: "1%",
          count: "36"
        },
        {
          name: "英语演讲班",
          teachers: ["徐旭才"],
          subject: "英语",
          time: "5.23-3.19",
          grade: "小学六年级",
          progress: "99%",
          count: "35"
        }
      ],
      calendarDate: ["2020-01-27", "2020-04-04", "2020-04-01", "2020-04-13"],
      studyTasks: [
        {
          time: "9:00",
          course: "编程思维训练班",
          task: "第五次直播课",
          status: "已结束"
        },
        {
          time: "14:00",
          course: "名家写作班",
          task: "风景描述",
          status: "进行中"
        },
        {
          time: "18:00",
          course: "英语演讲班",
          task: "外教Landy课",
          status: "未开始"
        },
        {
          time: "19:00",
          course: "英语演讲班",
          task: "小组讨论课",
          status: "未开始"
        }
      ]
    };
  },
  computed: {
    studyTimeProgress: function() {
      return (this.studyTime / this.planTime) * 100;
    }
  },
  onReady() {
    this.getClientHeight(0);
  },
  methods: {
    async tapChangeIndex(e) {
      this.currentIndex = e.target.dataset.index;
    },
    async swiperChangeIndex(e) {
      this.currentIndex = e.detail.current;
      this.getClientHeight(this.currentIndex);
    },
    async getClientHeight(id) {
      var query = uni.createSelectorQuery();
      var that = this;
      query.select(`.course-item-${id}`).boundingClientRect(function (rect) {
        that.clientHeight = rect.height;
      }).exec();
    },
    statusColor(status) {
      let color = "";
      switch (status) {
        case "未开始":
          break;
        case "进行中":
          color = "#4caf50";
          break;
        case "已结束":
          color = "#eb4559";
          break;
        default:
          break;
      }
      return color;
    }
  }
};
</script>

<style lang="stylus" scoped>
redColor = #eb4559
.course
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
    .swiper-item
      padding 0 5vw
    .my-class
      .study-time-card
        position relative
        margin 5px auto
        padding 5px 0
        box-shadow 0 0 5px 0 #E5EAF0
        border-radius 10px
        background-image url('http://photo-static-api.fotomore.com/creative/vcg/veer/612/veer-134067555.jpg')
        background-size cover
        .study-time-wrap
          position absolute
          top 50%
          left 50%
          transform translate(-50%, -50%)
          z-index 1
          width 80%
          height 95%
          border-radius 10px
          background-color rgba(255,255,255,0.6)
        .study-time-main
          position relative
          z-index 2
          height 130px
          display flex
          justify-content center
          .info
            position absolute
            top 50%
            left 50%
            transform translate(-50%, -50%)
            font-size 12px
        .study-time-footer
          position relative
          z-index 2
          text-align center
          line-height 30px
      .my-courses
        .head
          display flex
          justify-content space-between
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
                align-items flex-end
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
                .progress
                  .number
                    color redColor
                    padding-left 5px
                .count
                  color #666
                  font-size 13px
    .study-plan
      .study-task-wrap
        padding 0 5vw
        margin 10px 0
        .title
          font-weight bold
        .study-task
          display flex
          justify-content space-between
          line-height 50px
          border-bottom 1px dashed #e0e0e0
          .status
            color #999
            font-size 15px
</style>
