<template>
  <block>
    <view class="list-container">
      <view class="content" style="display: flex;align-items: center;">
        <view style="flex: 0 0 50px;">{{movie.index}}</view>
        <view class="view-title title" style="flex: 3 1 0%;">
          <text>{{movie.title}}</text>
        </view>
        <view class="author" style="flex: 1;">
          <!-- <text>{{movie.author_list[0].user_name}} —— </text> -->
          <!-- <text>{{movie.author_list[0].desc}}</text> -->
          <text>{{movie.heat}}</text>
        </view>
      </view>
      <view>
        <image style="width: 15px;height:15px;" class="avatar" :src="movie.img_url || 'https://petrify.oss-cn-beijing.aliyuncs.com/arrow-right.png'" />
      </view>
    </view>
    <!-- <block v-else>
      <view class="only-title title">
        <text>{{movie.title}}</text>
        <image class="arraw" src="https://petrify.oss-cn-beijing.aliyuncs.com/arrow-right.png" />
      </view>
    </block> -->
  </block>
</template>

<script>
export default {
  props: {
    movie: Object
  }
}
</script>

<style>
  .title {
    font-size: 28rpx;
    line-height: 40rpx;
    /* margin-bottom: 10rpx; */
    font-weight: bold;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }
  .only-title {
    height: 100%;
    line-height: 170rpx;
    text-align: left;
    padding-left: 20rpx;
    display: flex;
    align-items: center;
  }

  .only-title text {
    width: 680rpx;
  }

  .arraw {
    width: 28rpx;
    height: 28rpx;
  }

  .view-title {
    text-align: left;
  }

  .avatar {
    width: 100rpx;
    height: 100rpx;
    padding-right: 20rpx;
  }

  .list-container {
    display: flex;
    align-items: center;
    height: 100%;
    /* padding-left: 20rpx; */
  }

  .content {
    /* width: 600rpx; */
    flex: 1 1 80%;
  }

  .author {
    text-align: left;
    color: #979794;
  }
</style>

