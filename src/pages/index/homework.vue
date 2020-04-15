<template>
  <view class="homework">
    <view v-show="currentIndex == 0" class="upload-btn" @tap="handleUploadShow"
      >＋</view
    >
    <view class="upload-container" v-show="uploadShow">
      <view class="upload">
        <ul>
          <li class="btn" v-for="(item, index) in uploadBtns" :key="index">
            <view class="text">{{ item.title }}</view>
            <view class="icon"><img :src="item.icon" alt=""/></view>
          </li>
        </ul>
        <view style="color:#F66B0A;line-height:100rpx;">上传得榜样值</view>
        <view class="hiddenBtn" @tap="handleUploadHidden">x</view>
      </view>
    </view>
    <ul class="tabbar-wrap" @tap="tapChangeIndex">
      <li
        :data-index="index"
        :class="currentIndex == index ? 'active' : ''"
        v-for="(tab, index) in tabs"
        :key="tab"
      >
        {{ tab }}
      </li>
    </ul>
    <view class="contain-wrap">
      <view class="contain-classwork" v-show="currentIndex == 0">
        <view class="subjects" @tap="changeSubject">
          <view
            :class="['subject', currentSubjectIndex === i ? 'active' : '']"
            :data-index="i"
            v-for="(subject, i) in subjects"
            :key="i"
            >{{ subject }}</view
          >
        </view>
        <view class="ad">
          <img src="http://biyoung.xichi.xyz/homework/ad.jpg" />
        </view>
        <view class="homework-cards">
          <view
            class="homework-card"
            v-for="(item, index) in classwork"
            :key="index"
          >
            <view class="left">
              <view class="title">{{ item.title }}</view>
              <view class="detail">
                <view class="author">
                  <img :src="item.avatar" />
                  <view class="text name">{{ item.author }}</view>
                </view>
                <view class="like text"> {{ item.hit }}阅读量 </view>
              </view>
            </view>
            <view class="right">
              <img class="pic" :src="item.pic" />
              <view class="detail">
                <view class="comments">
                  <img
                    src="http://biyoung.xichi.xyz/icon/N-comments.png"
                    alt=""
                  />
                  <text>{{ item.comments }}</text>
                </view>
                <view class="like">
                  <img src="http://biyoung.xichi.xyz/icon/like.png" alt="" />
                  <text>{{ item.like }}</text>
                </view>
              </view>
            </view>
          </view>
        </view>
      </view>
      <view class="contain-exercise" v-show="currentIndex == 1">
        <view class="ad">
          <img src="http://biyoung.xichi.xyz/ad2.jpg" alt="" />
        </view>
        <view class="select-bar">
          <view
            class="dropdown"
            v-for="(list, index) in selectList"
            :key="index"
          >
            <view class="dropdown-title" @tap="handleselectedListShow"
              >{{ selectedList[index] }} ∨</view
            >
            <view class="dropdown-menu" v-show="selectedListShow">
              <view
                v-for="(item, i) in list"
                :key="i"
                @tap="changeSelectList(index, i)"
              >
                {{ item }}
              </view>
            </view>
          </view>
        </view>
        <view class="exercise-cards-wrap">
          <view
            class="exercise-cards"
            v-for="(item, index) in exerciseCards"
            :key="index"
          >
            <img :src="item.img" alt="" />
            <view class="card-part">
              <view style="font-weight:bold;font-size:15px;color:#000;">{{
                item.name
              }}</view>
              <view>正确率：{{ item.rate }}</view>
            </view>
            <view class="card-part">
              <view>已学：{{ item.progress }}</view>
              <view>排名：{{ item.rank }}</view>
            </view>
          </view>
        </view>
      </view>
      <view class="contain-reading-corner" v-show="currentIndex == 2">
        <view class="books-recommend">
          <view class="head">书目推荐</view>
          <view
            class="book-card"
            v-for="(book, index) in booksRecommend"
            :key="index"
          >
            <img :src="book.pic" alt="" />
            <view class="info">
              <view
                >{{ book.title
                }}<text style="color:#999;margin-left:5px;">|</text
                ><text style="color:#333;font-size:12px;margin-left:5px;">{{
                  book.author
                }}</text></view
              >
              <view style="display:flex;">
                <view v-for="i in book.rate" :key="i">★</view>
              </view>
              <view style="color:#C92B0C;font-size:14px;"
                >“{{ book.comments }}”</view
              >
            </view>
          </view>
        </view>
        <view class="reading-star-wrap">
          <view class="head"
            >阅读之星<text style="font-weight:300;margin-left:10px;"
              >（{{ readingStar.time }}）</text
            ></view
          >
          <view class="info">
            <view class="left">
              <img :src="readingStar.avatar" alt="" />
              <view style="margin-top:10px;text-align:center;">{{
                readingStar.name
              }}</view>
            </view>
            <view class="right">
              {{ readingStar.info }}
            </view>
          </view>
          <view class="btn">
            <text>全部内容赏析</text>
            <img
              src="http://biyoung.xichi.xyz/icon/%E6%89%8B%E6%8C%87%E4%B8%8A.png"
              alt=""
            />
          </view>
        </view>
      </view>
    </view>
  </view>
</template>

<script>
export default {
  comments: {},
  data() {
    return {
      currentIndex: 0,
      tabs: ["课堂作业", "习题课测评", "阅读角"],
      subjects: ["推荐", "习题", "作文", "试卷", "笔记", "手抄报", "读后感"],
      currentSubjectIndex: 0,
      classwork: [
        {
          title: "这是三年级语文反义词：记得给我点赞和收藏哈，谢谢了。",
          pic: "http://biyoung.xichi.xyz/banner/biyoung.jpg",
          hit: 3815,
          comments: 57,
          like: 259,
          author: "苏苏",
          avatar: "http://biyoung.xichi.xyz/avatar/avatar4.jpg"
        },
        {
          title: "叮咚—，你们要的笔记来了——三年级语文",
          pic: "http://biyoung.xichi.xyz/banner/biyoung2.jpg",
          hit: 3815,
          comments: 57,
          like: 259,
          author: "182****3250",
          avatar: "http://biyoung.xichi.xyz/avatar/avatar5.jpg"
        },
        {
          title: "字迹丑陋，请原谅——四年级英语",
          pic: "http://biyoung.xichi.xyz/banner/biyoung3.jpg",
          hit: 3815,
          comments: 57,
          like: 259,
          author: "182****3250",
          avatar: "http://biyoung.xichi.xyz/avatar/avatar6.jpg"
        },
        {
          title: "对你们来说，有帮助吗？——五年级数学",
          pic: "http://biyoung.xichi.xyz/banner/biyoung4.jpg",
          hit: 3815,
          comments: 57,
          like: 259,
          author: "182****3250",
          avatar: "http://biyoung.xichi.xyz/avatar/avatar7.jpg"
        },
        {
          title: "这是三年级语文反义词：记得给我点赞和收藏哈，谢谢了。",
          pic: "http://biyoung.xichi.xyz/banner/biyoung.jpg",
          hit: 3815,
          comments: 57,
          like: 259,
          author: "苏苏",
          avatar: "http://biyoung.xichi.xyz/avatar/avatar4.jpg"
        },
        {
          title: "叮咚—，你们要的笔记来了——三年级语文",
          pic: "http://biyoung.xichi.xyz/banner/biyoung2.jpg",
          hit: 3815,
          comments: 57,
          like: 259,
          author: "182****3250",
          avatar: "http://biyoung.xichi.xyz/avatar/avatar5.jpg"
        }
      ],
      uploadShow: false,
      uploadBtns: [
        {
          title: "作业批改",
          icon:
            "http://biyoung.xichi.xyz/course/icon/%E8%AF%BE%E7%A8%8B%E6%9F%A5%E8%AF%A2.png"
        },
        {
          title: "作业答疑",
          icon:
            "http://biyoung.xichi.xyz/course/icon/%E8%AF%BE%E7%A8%8B%E7%94%BB%E5%83%8F.png"
        },
        {
          title: "我来晒图",
          icon:
            "http://biyoung.xichi.xyz/course/icon/%E8%AF%BE%E7%A8%8B%E5%BD%A2%E5%BC%8F.png"
        }
      ],
      selectList: [
        ["一年级", "二年级", "三年级", "四年级", "五年级", "六年级"],
        ["语文", "数学", "英语", "科学"],
        ["上册", "下册"]
      ],
      selectedList: ["五年级", "数学", "上册"],
      selectedListShow: false,
      exerciseCards: [
        {
          img: "http://biyoung.xichi.xyz/homework/exerciseImg.jpg",
          name: "第一章：数的运算",
          rate: "100%",
          progress: "78%",
          rank: "1"
        },
        {
          img: "http://biyoung.xichi.xyz/homework/exerciseImg.jpg",
          name: "第二章：数的运算",
          rate: "100%",
          progress: "78%",
          rank: "1"
        },
        {
          img: "http://biyoung.xichi.xyz/homework/exerciseImg.jpg",
          name: "第三章：数的运算",
          rate: "100%",
          progress: "78%",
          rank: "1"
        },
        {
          img: "http://biyoung.xichi.xyz/homework/exerciseImg.jpg",
          name: "第四章：数的运算",
          rate: "100%",
          progress: "78%",
          rank: "1"
        },
        {
          img: "http://biyoung.xichi.xyz/homework/exerciseImg.jpg",
          name: "第五章：数的运算",
          rate: "100%",
          progress: "78%",
          rank: "1"
        },
        {
          img: "http://biyoung.xichi.xyz/homework/exerciseImg.jpg",
          name: "第六章：数的运算",
          rate: "100%",
          progress: "78%",
          rank: "1"
        }
      ],
      booksRecommend: [
        {
          pic: "http://biyoung.xichi.xyz/homework/book1.jpg",
          title: "平凡的世界",
          author: "路遥",
          rate: 5,
          comments: "深受老师和学生喜爱的新课标必读书"
        },
        {
          pic: "http://biyoung.xichi.xyz/homework/book2.jpg",
          title: "解忧杂货店",
          author: "东野圭吾",
          rate: 5,
          comments: "深受老师和学生喜爱的新课标必读书"
        },
        {
          pic: "http://biyoung.xichi.xyz/homework/book3.jpg",
          title: "老人与海",
          author: "海明威",
          rate: 5,
          comments: "深受老师和学生喜爱的新课标必读书"
        }
      ],
      readingStar: {
        time: "2020年5月",
        name: "小萌小可爱",
        avatar: "http://biyoung.xichi.xyz/avatar/avatar8.jpg",
        info:
          "人生就是一场没有止境的旅途，每个人手里只有一张白纸，而你是随心所欲在纸上描绘地图的人，未来有一切可能，而这一切全在于你自己......"
      }
    };
  },
  onLoad() {},
  methods: {
    tapChangeIndex(e) {
      this.currentIndex = e.target.dataset.index;
    },
    changeSubject(e) {
      this.currentSubjectIndex = e.target.dataset.index;
    },
    handleUploadShow() {
      this.uploadShow = true;
    },
    handleUploadHidden() {
      this.uploadShow = false;
    },
    handleselectedListShow() {
      this.selectedListShow = !this.selectedListShow;
    },
    changeSelectList(index, i) {
      this.selectedList[index] = this.selectList[index][i];
      this.selectedList.push("");
      this.selectedList.pop();
      this.handleselectedListShow();
    }
  }
};
</script>

<style lang="stylus" scoped>
.homework
  position relative
  .upload-btn
    position fixed
    bottom 50rpx
    right 50rpx
    width 60px
    height 60px
    border-radius 50%
    background-color #E9BF6C
    text-align center
    line-height 50px
    font-size 60px
    color #4e342e
    font-weight bold
    z-index 100
  .upload-container
    position fixed
    width 100vw
    height 100vh
    background-color #FFF
    z-index 200
    .upload
      position absolute
      right 100rpx
      bottom 150rpx
      .btn
        display flex
        margin-top 20px
        .text
          line-height 50px
          margin-right 5px
        .icon
          position relative
          width 50px
          height 50px
          border-radius 50%
          background-color #E9BF6C
          img
            position absolute
            width 30px
            height 30px
            top 50%
            left 50%
            transform translate(-50%, -50%)
      .hiddenBtn
        margin-right 30rpx
        font-size 50rpx
        font-weight bold
        color #4e342e
        float right
  .tabbar-wrap
    display flex
    justify-content space-between
    padding 5px 5vw
    line-height 40px
    border-bottom 1px solid #999
    .active
      color #eb4559
      font-weight bold
  .contain-wrap
    background-color #FFF
    .contain-classwork
      position relative
      .subjects
        display flex
        padding 0 5vw
        padding-top 5px
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
          background-color #EB701A
          color #ffffff
          border 1px solid #EB701A
      .ad
        height 100px
        width 100%
        display flex
        justify-content center
        align-items center
        border-bottom 1px solid #666
        img
          width 90%
          height 80%
          margin 0 auto
          border-radius 5px
      .homework-cards
        .homework-card
          display flex
          justify-content space-between
          padding 10rpx 30rpx
          height 100px
          border-bottom 1px solid #999
          .left
            display flex
            flex-direction column
            justify-content space-between
            .detail
              display flex
              justify-content space-between
              font-size 12px
              color #666
              width 62vw
              .text
                line-height 30px
              .author
                display flex
                img
                  width 30px
                  height 30px
                  border-radius 50%
                .name
                  margin-left 5px
          .right
            display flex
            flex-direction column
            justify-content space-between
            .pic
              width 90%
              height 80%
              margin 0 auto
              border-radius 10px
            .detail
              display flex
              justify-content space-around
              font-size 12px
              width 28vw
              margin 5px 0
              color #333
              img
                width 15px
                height 15px
              text
                margin-left 5px
    .contain-exercise
      .ad
        height 150px
        width 100%
        display flex
        justify-content center
        align-items center
        img
          width 90%
          height 80%
          margin 0 auto
          border-radius 5px
      .select-bar
        display flex
        justify-content space-around
        padding 10px 0
        border-top 1px solid #999
        border-bottom 1px solid #999
        .dropdown
          position relative
          .dropdown-title
            font-weight bold
          .dropdown-menu
            position absolute
            top 33px
            left -30px
            background-color #F4F5F6
            padding 5px 10px 10px 10px
            width 80px
            text-align center
            border-radius 10px
            box-shadow 0 0 15px 0 rgba(#999, .5)
      .exercise-cards-wrap
        .exercise-cards
          display flex
          justify-content space-around
          padding 20px 10px
          border-bottom 1px solid #999
          background-color #E0ECF2
          img
            width 100px
            height 80px
          .card-part
            display flex
            flex-direction column
            justify-content center
            color #333
            font-size 13px
            > view
              margin-bottom 10px
    .contain-reading-corner
      background-color #E0ECF2
      padding-bottom 10px
      .books-recommend
        background-color #ffffff
        width 95vw
        border 1px solid #BBBBBB
        border-radius 5px
        margin 0 auto
        .head
          font-weight bold
          padding-left 50rpx
          line-height 50rpx
        .book-card
          display flex
          justify-content space-around
          align-items center
          height 150px
          width 80%
          margin 0 auto
          border-bottom 1px dashed #999
          &:last-of-type
            border none
          img
            width 80px
            height 80px
          .info
            margin-left 20px
            >view
              margin-bottom 5px
      .reading-star-wrap
        background-color #ffffff
        width calc(95vw - 20px)
        border 1px solid #BBBBBB
        border-radius 5px
        margin 20rpx auto
        padding 20px 10px
        .head
          font-weight bold
        .info
          width 80%
          margin 50rpx auto
          display flex
          justify-content space-between
          .left
            img
              width 100px
              height 100px
              border-radius 50%
          .right
            text-indent 2em
            margin-left 20px
        .btn
          border 1px solid #bbbbbb
          border-radius 10px
          text-align center
          width 180px
          height 30px
          line-height 30px
          margin 0 auto
          display flex
          align-items center
          justify-content center
          img
            width 20px
            height 20px
</style>
