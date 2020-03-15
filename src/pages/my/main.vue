<template>
  <!-- <div class="container">
    <image class="cover" :src="data.hp_img_url" mode="widthFix" />
    <view class="cover-author">
      <text class="gray">{{data.hp_author}}</text>
    </view>
    <view class="content">
      <text>{{content}}</text>
    </view>
    <view class="content-author">
      <text class="gray">{{data.text_authors}}</text>
    </view>
  </div> -->
  <div style="min-height: calc(100vh - 94px);background: #efefef;">
    <div style="display: flex;align-items: center;padding: 20px;background: #fff;margin-bottom: 20px;">
      <div><img style="width: 50px;border-radius: 50%;border: 1px #d2d2d2 solid;" src="static/assert/music.png" alt=""></div>
      <div style="padding-left: 20px;display: flex;flex-direction: column;">
        <div>bilibili</div>
        <div style="font-size: 15px;color: #888;">UUID: liulinboyi</div>
      </div>
    </div>
    <div style="padding: 20px 0;color: #888;padding: 20px;background: #fff;border-bottom: 1px #efefef solid;">
      收藏
    </div>
    <div style="padding: 20px 0;color: #888;padding: 20px;background: #fff;border-bottom: 1px #efefef solid;">
      设置
    </div>
    <div @click="quite" style="padding: 20px 0;color: #888;padding: 20px;background: #fff;">
      退出
    </div>
    <div style="margin-top: 100px;margin-top: 100px;text-align: center;color: #888;">
      v1.0
    </div>
  </div>
</template>

<script>
import { mapState, mapActions } from 'vuex'
import auth from '../../utils/auth';
export default {
  mounted() {
    this.initPage()
  },
  mixins: [auth],
  components: {
  },
  computed: {
    ...mapState('home', ['data']),
    ...mapState('weather', ['weather']),
    content() {
      return this.data.hp_content.split('by')[0]
    }
  },
  methods: {
    ...mapActions('home', ['getNewIds', 'getHomeData']),
    async initPage() {
      await this.getNewIds()
      await this.getHomeData()
    },
    quite() {
      uni.showModal({
        title: '提示',
        content:'您确定要退出吗？',
        success(e) {
          console.log(e);
          if (e.confirm) {
           uni.removeStorageSync('userInfo')
            uni.navigateTo({
              url: '/pages/login/main'
            })
          }
        }
      })
    }
  }
}
</script>

<style scoped>
  .cover {
    width: 100%;
  }
  .cover-author {
    width: 100%;
    height: 100rpx;
    line-height: 100rpx;
    margin-bottom: 30rpx;
  }
  .content {
    width: 80%;
    margin: 0 auto;
    line-height: 58rpx;
    text-align: left;
  }
  .content-author {
    height: 100rpx;
    line-height: 100rpx;
    font-size: 20rpx;
  }
</style>
