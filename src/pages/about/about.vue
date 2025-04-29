<template>
  <view class="container">
      <view class="profile">
        <view class="profile-avatar">
          <image :src="user.avatar" mode="aspectFill"></image>
        </view>
        <view class="profile-info">
          <text class="nickname">{{ user.nickname }}</text>
          <text class="bio">{{ user.bio }}</text>
        </view>
      </view>

    <uni-section title="功能菜单" type="line" :shadow="false">
      <view class="function-list">
        <view class="function-item">
          <uni-icons class="icons" type="gear-filled"></uni-icons>
          <text class="function-text">设置</text>
        </view>
        <view class="function-item">
          <uni-icons class="icons" type="chat-filled"></uni-icons>
          <text class="function-text">消息</text>
        </view>
        <view class="function-item">
          <uni-icons class="icons" type="info-filled"></uni-icons>
          <text class="function-text">关于</text>
        </view>
      </view>
    </uni-section>
  </view>
</template>

<script lang="ts">
import { ref } from 'vue';

class UserInfo {
  nickname: string = '';
  bio: string = '';
  avatar: string = '';
  constructor(nickname: string, avatar?: string ,bio?: string) {
    this.nickname = nickname;
    this.avatar = avatar || ''
    this.bio = bio || ''
  }
}

export default {
  setup() {
    let user = ref<UserInfo>(new UserInfo(
        '测试账号',
        '/static/default-avatar.jpeg',
        '你好~~~'))

    return {
      user
    };
  },
};
</script>

<style>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.profile {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 100vw;
  background-color: #dce1e8;
  padding: 30px 0 ;
}

.profile-avatar {
  width: 100px;
  height: 100px;
  border-radius: 60px;
  overflow: hidden;
  margin-bottom: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.profile-avatar image {
  width: 100%;
  height: 100%;
}

.profile-info {
  display: flex;
  flex-direction: column;
  text-align: center;
}

.nickname {
  font-size: 18px;
  width: 100vw;
  font-weight: bold;
  margin-bottom: 10px;
  color: #333;
}

.bio {
  width: 100vw;
  font-size: 14px;
  color: #666;
}

.function-list {
  width: 100vw;
}

.function-item {
  display: flex;
  align-items: center;
  padding: 15px 0;
  border-bottom: 1px solid #ddd;
}

.function-text {
  font-size: 16px;
  color: #333;
}

.icons {
  margin: 2px 10px 0 10px;
}
</style>
