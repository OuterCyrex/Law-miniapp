<template>
  <view class="container">
    <view class="swiper-container">
      <uni-swiper-dot :info="swiperList" :current="currentIndex" field="src" mode="default">
        <swiper class="swiper-box" @change="swiperChange" :autoplay="true">
          <swiper-item v-for="(item, index) in swiperList" :key="index">
            <view class="swiper-item">
              <image :src="item.src" mode="aspectFill" />
            </view>
          </swiper-item>
        </swiper>
      </uni-swiper-dot>
    </view>

    <view class="notice-bar" style="margin-top: 0">
      <text>🔔 功能一览</text>
    </view>

    <view class="nav-icons">
      <view
          class="nav-item"
          v-for="(item, index) in navItems"
          :key="index"
      >
        <view class="icon-wrapper" :style="{ backgroundColor: item.bgColor }">
          <image :src="item.icon" mode="aspectFill" class="icon" />
        </view>
        <text class="nav-text">{{ item.text }}</text>
      </view>
    </view>

    <view class="notice-bar">
      <text>🎉 平台访问量</text>
    </view>

    <!-- 三个指标 -->
    <view class="stats-container">
      <uni-card class="stat-card" v-for="(stat, index) in stats" :key="index">
        <text class="stat-number" style="margin-right: 5px">{{ stat.value }}</text>
        <text class="stat-label">{{ stat.label }}</text>
      </uni-card>
    </view>

    <view class="notice-bar">
      <text>📚 常见问题</text>
    </view>

    <view class="faq-list">
      <view class="faq-item" v-for="(item, index) in faqList" :key="index">
        <text class="faq-question">{{ item }}</text>
        <uni-icons type="right" size="18" color="#999" />
      </view>
    </view>

  </view>
</template>

<script lang="ts" setup>
import { ref } from 'vue'

let currentIndex = ref<number>(0)

const swiperChange = (e: any) => {
  currentIndex.value = e.detail.current
}

const swiperList = ref([
  { src: 'https://outer-pictures.oss-cn-beijing.aliyuncs.com/law/1.png' },
  { src: 'https://outer-pictures.oss-cn-beijing.aliyuncs.com/law/2.png' },
])

const navItems = ref([
  {
    text: '专家咨询',
    page: '/pages/expert/expert',
    icon: 'https://img.icons8.com/?size=100&id=P7HpRDNHXCyg&format=png&color=000000',
    bgColor: '#3a86ff44',
  },
  {
    text: 'AI对话',
    page: '/pages/ai/ai',
    icon: 'https://img.icons8.com/?size=100&id=gpyVo2fNonq4&format=png&color=000000',
    bgColor: '#2ecc7144',
  },
  {
    text: '在线建议',
    page: '/pages/advice/advice',
    icon: 'https://img.icons8.com/?size=100&id=ZAASfo9L21mn&format=png&color=000000',
    bgColor: '#e6394644',
  },
  {
    text: '我的',
    page: '/pages/about/about',
    icon: 'https://img.icons8.com/?size=100&id=21838&format=png&color=000000',
    bgColor: '#f4a26144',
  },
])

const stats = ref([
  { label: '浏览量', value: 25678 },
  { label: '收藏量', value: 5432 },
  { label: '使用量', value: 19876 },
])

const faqList = ref([
  '如何提交法律问题？',
  '平台如何保障隐私？',
  'AI问答是否收费？',
  '专家答复要多久？'
])
</script>

<style scoped lang="scss">
.container {
  background-color: #f4f4f4;
  min-height: 100vh;
}

.swiper-image {
  width: 100%;
  height: 160px;
}

.notice-bar {
  font-size: 14px;
  margin-top: 10px;
  padding: 10px 20px;
  background-color: white;
  color: #333;
}

.nav-icons {
  background-color: white;
  display: flex;
  justify-content: space-between;
  padding-bottom: 20px;
}

.nav-item {
  flex: 1;
  align-items: center;
  justify-content: center;
  text-align: center;
  cursor: pointer;
}

.icon-wrapper {
  width: 60px;
  height: 60px;
  border-radius: 50%;
  margin: 0 auto 6px;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 4px 8px rgba(0,0,0,0.1);
}

.icon {
  width: 36px;
  height: 36px;
}

.nav-text {
  font-size: 13px;
  color: #555;
}

.stats-container {
  padding: 1px 10px 10px 10px;
  background-color: white;
}

.stat-card {
  background-color: #f9fafb;
  border-radius: 10px;
  text-align: center;
  box-shadow: 0 2px 6px #f0f1f5;
  cursor: default;
}

.stat-number {
  font-size: 22px;
  font-weight: 700;
  color: #58ad43;
}

.stat-label {
  font-size: 14px;
  color: #666;
}

.section-title {
  font-size: 16px;
  font-weight: 700;
  padding-bottom: 8px;
  border-left: 4px solid #3a86ff;
  margin-bottom: 10px;
  color: #222;
}

.case-list {
  display: flex;
  flex-direction: row;
  overflow-x: scroll;
  padding-bottom: 12px;
  gap: 12px;
}

.case-card {
  width: 140px;
  height: 100px;
  border-radius: 12px;
  overflow: hidden;
  flex-shrink: 0;
  box-shadow: 0 4px 8px rgb(0 0 0 / 0.08);
  cursor: pointer;
}

.case-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.faq-list {
  background: white;
  border-radius: 10px;
  overflow: hidden;
}

.faq-item {
  padding: 14px 16px;
  border-bottom: 1px solid #eee;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.faq-item:last-child {
  border-bottom: none;
}

.faq-question {
  font-size: 14px;
  color: #333;
}

.swiper-container {
  height: 150px;
  z-index: 10;
}
.swiper-item {
  height: 100%;
}
.swiper-item image {
  width: 100%;
  height: 100%;
}
</style>
