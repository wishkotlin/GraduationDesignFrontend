<template>
  <div class="container" style="padding-top: 135px;">
    <!-- <image class="cover" :src="data.hp_img_url" mode="widthFix" />
    <view class="cover-author">
      <text class="gray">{{data.hp_author}}</text>
    </view>
    <view class="content">
      <text>{{content}}</text>
    </view>
    <view class="content-author">
      <text class="gray">{{data.text_authors}}</text>
    </view> -->
    <!-- <div style="margin: 0 auto;padding: 25px;font-size: 20px;">登录</div> -->
    <div style="display: flex;align-items: center;padding: 20px;"><span style="font-size: 15px;">注册：</span><input
        style="text-align: left;flex: 1;outline: 1px #cecece solid;"
        type="text"
        v-model="name"
      ></div>
    <div style="display: flex;align-items: center;padding: 20px;"><span style="font-size: 15px;">密码：</span><input
        style="text-align: left;flex: 1;outline: 1px #cecece solid;"
        type="password"
        v-model="passwd"
      ></div>
    <button style="width: 25%;" @click="login">登录</button>
  </div>
</template>

<script>
import { mapState, mapActions } from 'vuex'
import auth from '../../utils/auth';
export default {
  data() {
    return {
      name: '',
      passwd: ''
    }
  },
  mixins: [auth],
  mounted() {
    this.initPage()
    let userInfo = uni.getStorageSync('userInfo')
    console.log(userInfo);
    
    if (userInfo) {
      this.name = userInfo.name
      this.passwd = userInfo.passwd
      this.login()
    }
  },
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
    login() {
      if (this.name.length < 6 || this.passwd.length < 6) {
        uni.showModal({
          title: "提示",
          content: "用户名密码需要大于6位",
          showCancel: false
        })
        return;
      }
      uni.setStorageSync('userInfo', {
        name: this.name,
        passwd: this.passwd
      })
      uni.switchTab({
        url: '/pages/my/main'
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
