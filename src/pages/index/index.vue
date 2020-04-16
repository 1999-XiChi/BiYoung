<template>
  <view class="index">
	<view class="search-box">
    <input class="search" type="text" placeholder="搜索你感兴趣的课程~" @tap="tapSearchBox">
    <img class="icon" src="http://biyoung.xichi.xyz/icon/search.png">
  </view>
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
          <view class="swiper-item hot-courses index-item-0">
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
          <view class="index-item growth-example index-item-1">
            <view class="growth-example-wrap">
              <view class="title">
                <text>成长榜样</text>
                <text class="more">更多>></text>
              </view>
              <view class="main">
                <view class="item" v-for="(example, index) in growthExamples" :key="index">
                  <view class="rank" :style="{color: rankColor[example.rank - 1]}">{{example.rank}}.</view>
                  <img class="avatar" :src="example.avatar"></img>
                  <view class="info">
                    <view class="info-header">
                      <text style="font-size:15px;font-weight:bold;">{{example.name}}</text>
                      <view>
                        <text style="color:#f44336;padding-left:20px;font-size:13px;">{{example.score}}</text>
                        <text style="color:#666;padding-left:5px;font-size:12px;">榜样值</text>
                      </view>
                    </view>
                    <view>{{example.comment}}</view>
                  </view>
                </view>
              </view>
            </view>
            <view class="hot-dairy-wrap">
              <view class="title">
                <text>心情故事</text>
                <text class="more">更多>></text>
              </view>
              <view class="main">
                <view class="item" v-for="(dairy, index) in hotDairies" :key="index">
                  <view class="rank" :style="{color: rankColor[dairy.rank - 1]}">{{dairy.rank}}.</view>
                  <img class="dairy-img" :src="dairy.img">
                  <view class="info">
                    <view class="info-header">
                      <view class="title">
                        <text>{{dairy.title}}</text>
                      </view>
                      <view class="sub-info">
                        <text>作者:{{dairy.author}}</text>
                        <text style="padding-left:5px;">日期:{{dairy.date}}</text>
                      </view>
                    </view>
                    <view class="text">{{dairy.text}}</view>
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
          <view class="about-us index-item-2">
            <swiper indicator-dots autoplay class="banner-wrap">
              <swiper-item
                v-for="(item, index) in biyoungBanner"
                :key="index"
                class="banner"
              >
                <view
                  class="banner-bg"
                  :style="{ backgroundImage: `url(${item})` }"
                ></view>
              </swiper-item>
            </swiper>
              <view class="info-wrap">
                <view class="bg"></view>
                <view class="info">飞扬工作室（简称“BiYoung”）是一家专业以教育咨询为主的创新教育信息科技公司。飞扬工作室依托南京市社会培训行业协会栖霞分会提供栖霞区教育兼职信息。公司自2019年9月5日创办以来，一直致力于筛选、面试、培训有兼职需求的大学生，向教育机构高效输送中长期兼职教师。公司始终以“诚信、优质、高效”为宗旨，以“全心服务、高效沟通”为团队精神，并逐步形成一套较为完备的筛选、面试、培训、管理的一站式服务体系。
托教项目是飞扬工作室2020年度启动的新一轮教育项目，本项目面向于小学一年级至六年级的学生，结合当前教育现状，我们致力于研发一套适合于小学生的晚托一体化服务体系，通过对不同年龄和性格等的学生的需求调查，适配出对应托教方案，从而引导学生在提高学习成绩的基础上，进一步实现多方面多层次的全面发展，响应素质教育的号召。</view>
                <view class="contact">
                  <view><text style="font-weight:bold;">联系电话：</text>19867205619 王女士</view>
                  <view><text style="font-weight:bold;">地址：</text>江苏省南京市亚东新城区文苑路9号</view>
                </view>
              </view>
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
          text: "一元体验课",
          color: "#eb4559"
        },
        {
          icon:
            "http://biyoung.xichi.xyz/course/icon/%E8%AF%BE%E7%A8%8B%20%281%29.png",
          text: "个性化师资匹配",
          color: "#084177"
        },
        {
          icon:
            "http://biyoung.xichi.xyz/course/icon/%E8%AF%BE%E7%A8%8B%E8%A1%A8.png",
          text: "沉浸式自习室",
          color: "#ffae8f"
        },
        {
          icon:
            "http://biyoung.xichi.xyz/course/icon/%E8%AF%BE%E7%A8%8B%20%282%29.png",
          text: "live直播",
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
      subjects: ["热门","兴趣","微课","综合","语文", "数学", "英语"],
      currentSubjectIndex: 0,
      courseCards: [
        {
          name: "托教“3+1”综合班",
          teachers: ["王坤", "胡里山"],
          subject: "综合",
          time: "4.23-9.19",
          grade: "小学六年级",
          cost: "99",
          count: "66"
        },
        {
          name: "珠心算进阶班",
          teachers: ["闻喜想"],
          subject: "数学",
          time: "4.23-5.19",
          grade: "小学六年级",
          cost: "199",
          count: "36"
        },
        {
          name: "写作进阶班",
          teachers: ["徐旭才"],
          subject: "语文",
          time: "5.23-3.19",
          grade: "小学六年级",
          cost: "599",
          count: "35"
        },
        {
          name: "模拟联合国（体验课）",
          teachers: ["王坤", "胡里山"],
          subject: "兴趣",
          time: "4.23-9.19",
          grade: "小学六年级",
          cost: "99",
          count: "66"
        }
      ],
      growthExamples: [{
        name: "红领巾侠",
        avatar: "http://biyoung.xichi.xyz/avatar/avatar1.jpg",
        comment: "千万别迷恋网络游戏，要玩就玩好人生这场大游戏。",
        score: 386,
        rank: 1
      },{
        name: "何同学",
        avatar: "http://biyoung.xichi.xyz/avatar/avatar2.jpg",
        comment: "没有一种不通过蔑视、忍受和奋斗就可以征服的命运。",
        score: 357,
        rank: 2
      },{
        name: "死灵法师",
        avatar: "http://biyoung.xichi.xyz/avatar/avatar3.jpg",
        comment: "我要像一块石灰一样活着别人越泼我凉水我的人生越沸腾。",
        score: 321,
        rank: 3
      }],
      hotDairies: [{
        title: "记海南之旅",
        author: "西池",
        img: "http://biyoung.xichi.xyz/dairy/dairy2.jpg",
        text: "我是正文我是正文我是正文。我是正文我是正文我是正文。我是正文我是正文我是正文。",
        date: "2020/04/12",
        rank: 1
      },{
        title: "我谈《水浒传》",
        author: "neko",
        img: "http://biyoung.xichi.xyz/dairy/dairy3.jpg",
        text: "我是正文我是正文我是正文。我是正文我是正文我是正文。我是正文我是正文我是正文。",
        date: "2020/04/10",
        rank: 2
      },{
        title: "寻找春天的踪迹",
        author: "hlszd",
        img: "http://biyoung.xichi.xyz/dairy/dairy1.jpg",
        text: "我是正文我是正文我是正文。我是正文我是正文我是正文。我是正文我是正文我是正文。",
        date: "2020/04/08",
        rank: 3
      }],
      rankColor:["#f44336","#e91e63","#9c27b0","#f6d186"],
      clientHeight: 0,
      biyoungBanner:[
        "http://biyoung.xichi.xyz/banner/biyoung2.jpg",
        "http://biyoung.xichi.xyz/banner/biyoung3.jpg",
        "http://biyoung.xichi.xyz/banner/biyoung4.jpg",
        "http://biyoung.xichi.xyz/banner/biyoung.jpg"
      ]
    };
  },
  onReady() {
    this.getClientHeight(0);
  },
  methods: {
    tapSearchBox(){
      uni.navigateTo({
        url: "/pages/search/search",
      });
    },
    async tapChangeIndex(e) {
      this.currentIndex = e.target.dataset.index;
    },
    async swiperChangeIndex(e) {
      this.currentIndex = e.detail.current;
      this.getClientHeight(this.currentIndex);
    },
    async changeSubject(e) {
      this.currentSubjectIndex = e.target.dataset.index;
      if(this.currentSubjectIndex == 1){
        this.courseCards = [{
          name: "智力开发课程",
          teachers: ["王坤", "胡里山"],
          subject: "兴趣",
          time: "4.23-9.19",
          grade: "小学六年级",
          cost: "99",
          count: "66"
        },
        {
          name: "好习惯养成课",
          teachers: ["闻喜想"],
          subject: "兴趣",
          time: "4.23-5.19",
          grade: "小学六年级",
          cost: "199",
          count: "36"
        }]
      }else if(this.currentSubjectIndex == 2){
        this.courseCards = [{
          name: "鸡兔同笼问题",
          teachers: ["王坤", "旬值"],
          subject: "微课",
          time: "4.23-9.19",
          grade: "小学六年级",
          cost: "99",
          count: "66"
        },
        {
          name: "路程问题（上）相遇问题",
          teachers: ["闻喜想"],
          subject: "微课",
          time: "4.23-5.19",
          grade: "小学六年级",
          cost: "199",
          count: "36"
        },{
          name: "路程问题（下）追及问题",
          teachers: ["陆旬值"],
          subject: "微课",
          time: "4.23-5.19",
          grade: "小学六年级",
          cost: "199",
          count: "36"
        }]
      }else{
        this.courseCards =  [
          {
            name: "托教“3+1”综合班",
            teachers: ["王坤", "胡里山"],
            subject: "综合",
            time: "4.23-9.19",
            grade: "小学六年级",
            cost: "99",
            count: "66"
          },
          {
            name: "珠心算进阶班",
            teachers: ["闻喜想"],
            subject: "数学",
            time: "4.23-5.19",
            grade: "小学六年级",
            cost: "199",
            count: "36"
          },
          {
            name: "写作进阶班",
            teachers: ["徐旭才"],
            subject: "语文",
            time: "5.23-3.19",
            grade: "小学六年级",
            cost: "599",
            count: "35"
          },
          {
            name: "模拟联合国（体验课）",
            teachers: ["王坤", "胡里山"],
            subject: "兴趣",
            time: "4.23-9.19",
            grade: "小学六年级",
            cost: "99",
            count: "66"
          }
        ]
        this.$nextTick(function(){
          this.getClientHeight(0);
        });
      }
    },
    async getClientHeight(id) {
      var query = uni.createSelectorQuery();
      var that = this;
      query.select(`.index-item-${id}`).boundingClientRect(function (rect) {
        that.clientHeight = rect.height;
      }).exec();
    }
  }
};
</script>

<style lang="stylus" scoped>
redColor = #eb4559
.index
  background-color #FDFDFD
  .search-box
    position relative
    width 80%
    height 30px
    margin 5px auto
    .search
      background-color #F7F7F7
      border-radius 20px
      padding 2px 10px
      font-size 12px
    .icon
      width 20px
      height 20px
      position absolute
      top 50%
      right 20px
      transform translateY(-50%)
  .indicator-wrap
    padding 0 20px 20px 20px
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
              margin 6rpx 8rpx
              padding 6rpx 12rpx
              font-size 10px
              border 1px solid #666
              border-radius 12px
              color #666
              &:first-child
                margin-left -1px
            .active
              background-color redColor
              border 1px solid redColor
              color #ffffff
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
    .growth-example
      .title
        font-weight bold
        display flex
        justify-content space-between
        align-item center
        .more
          font-size 12px
          color #666
      .main
        .item
          display flex
          height 80px
          align-items center
          .rank
            width 15px
            font-size 18px
            font-weight bold
          .avatar
            width 60px
            height 60px
            border-radius 50%
            box-shadow 0 0 5px 0 #aaa
            margin 0 10px
          .info
            width calc(90vw - 75px)
            .info-header
              display flex
              justify-content space-between
      .growth-example-wrap
        margin-bottom 50rpx
      .hot-dairy-wrap
        .item
          height 120px
          .dairy-img  
            width 180px
            height 100px
            border-radius 10px
            box-shadow 0 0 5px 0 #aaa
            margin 0 10px
          .info
            .info-header
              display inherit
              .title
                font-weight bold
              .sub-info
                color #333
                font-size 12px
            .text
              font-size 12px
              color #999
    .about-us
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
            background-size cover
      .info-wrap
        padding 0 5vw
        margin-top 10px
        position relative
        .bg
          position absolute
          top 50%
          left 50%
          transform translate(-50%, -50%)
          z-index -1
          width 150px
          height 255px
          background-image url('http://biyoung.xichi.xyz/logo.png')
          opacity 0.15
        .info
          text-indent 2em
        .contact
          margin-top 5px
</style>
