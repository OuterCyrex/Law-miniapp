<template>
  <view class="container">
    <view class="cards-container">
      <uni-card
          class="card"
          padding="0"
          spacing="0"
          margin="10px"
          shadow="0px 0px 3px 1px rgba(0, 0, 0, 0.08)"
          v-for="(c, i) in parts"
          :key="i"
      >
        <template v-slot:cover>
          <view class="custom-cover">
            <image class="cover-image" mode="aspectFill" :src="c.img">
            </image>
            <view class="cover-content">
              <text class="uni-subtitle">{{ c.title }}</text>
            </view>
          </view>
          <uni-list :border="false">
            <view @click="popup.open('bottom')">
              <uni-list-item title="点击在线咨询" showArrow></uni-list-item>
            </view>
          </uni-list>
        </template>
      </uni-card>
    </view>

    <view>
      <uni-popup ref="popup">
        <scroll-view :scroll-y="true" class="popup-content" type="bottom">
          <view class="header">
            <view class="title">网络安全建议</view>
            <text class="subtitle">保护你的数字生活</text>
          </view>
          <view class="introduction">
            <text class="intro-text">
              在当今数字化时代，网络安全变得尤为重要。随着互联网的普及，我们的个人信息、财务数据和在线活动都面临着各种安全威胁。网络安全不仅关乎个人隐私，还涉及到我们的财产安全和社会稳定。了解和采取适当的网络安全措施，可以帮助我们有效防范网络攻击，保护我们的数字生活。
            </text>
          </view>
          <view class="suggestions">
            <view class="section-title">网络安全建议</view>
            <view
                v-for="(suggestion, index) in suggestions"
                :key="index"
                class="suggestion-item"
            >
              <view class="suggestion-title">{{ index + 1 }}. {{ suggestion.title }}</view>
              <text class="suggestion-detail">{{ suggestion.detail }}</text>
            </view>
          </view>
          <view class="additional-info">
            <view class="section-title">网络安全日</view>
            <text class="info-text">
              每年的 9 月 28 日是国家网络安全日，这一天旨在提高公众对网络安全的意识，促进全社会共同参与网络安全建设。通过各种宣传活动和教育课程，我们可以更好地了解网络安全的重要性，并采取实际行动保护自己和他人的数字安全。
            </text>
          </view>
        </scroll-view>
      </uni-popup>
    </view>
  </view>
</template>

<script setup lang="ts">
import { ref } from 'vue'

class AdvicePart {
  img: string = ''
  title: string = ''

  constructor(title: string, img: string='') {
    this.img = img
    this.title = title
  }
}

const popup = ref<any | null>(null)

let parts = ref<Array<AdvicePart>>(
    [
      new AdvicePart('校园安全', '/static/adviceCover/school-security.jpeg'),
      new AdvicePart('网络保护', '/static/adviceCover/network-security.jpeg'),
      new AdvicePart('家庭权益', '/static/adviceCover/family-right.jpeg'),
      new AdvicePart('财务丢失', '/static/adviceCover/lost-found.png'),
      new AdvicePart('校园欺凌', '/static/adviceCover/school-bully.png'),
    ]
)

const suggestions = [
  {
    title: '使用强密码',
    detail: '确保你的密码包含大小写字母、数字和特殊字符，避免使用容易猜测的密码。建议定期更换密码，并使用密码管理器来帮助记忆复杂的密码。',
  },
  {
    title: '定期更新软件',
    detail: '操作系统和应用程序的更新通常包含重要的安全补丁。保持这些软件的最新版本，可以有效防止安全漏洞被利用。定期检查并安装更新，确保你的设备始终处于最佳安全状态。',
  },
  {
    title: '警惕网络钓鱼',
    detail: '网络钓鱼是一种常见的网络诈骗手段，攻击者通过伪装成可信的网站或邮件，诱骗用户提供个人信息。不要点击不明链接或下载不明来源的附件，避免个人信息泄露。在输入敏感信息前，务必确认网站的合法性。',
  },
  {
    title: '使用安全网络',
    detail: '公共 Wi-Fi 网络通常不够安全，容易被攻击者监听或篡改数据。避免在公共 Wi-Fi 下进行敏感操作，如网上银行或个人账户登录。如果需要使用公共网络，建议使用虚拟私人网络（VPN）来保护你的网络活动。',
  },
  {
    title: '启用双因素认证',
    detail: '双因素认证（2FA）为你的账户添加了额外的安全层。即使密码被盗，攻击者也无法访问你的账户，因为他们还需要通过另一层验证（如手机验证码或指纹识别）。建议在支持 2FA 的服务上启用此功能。',
  },
  {
    title: '定期备份数据',
    detail: '数据丢失可能是由于硬件故障、恶意软件或人为错误引起的。定期备份重要数据，确保在发生意外时能够快速恢复。可以使用云存储服务或外部硬盘进行备份。',
  },
  {
    title: '使用安全的浏览器扩展',
    detail: '安装并使用安全的浏览器扩展，如广告拦截器和隐私保护工具，可以提高你的上网体验并保护你的隐私。确保从官方渠道下载扩展，并定期更新以获取最新功能和安全补丁。',
  },
  {
    title: '保护个人信息',
    detail: '不要在不安全的网站上输入个人信息，确保网站使用 HTTPS 协议。避免在社交媒体上过度分享个人信息，以免被不法分子利用。',
  },
  {
    title: '使用虚拟私人网络 (VPN)',
    detail: '在公共网络环境下，使用 VPN 来保护你的网络活动不被窃听。VPN 可以加密你的网络连接，确保数据传输的安全性。',
  },
]
</script>


<style scoped lang="scss">
.container {
  height: 100vh;
  padding: 0 10px;
}
.cards-container {
  display: grid;
  grid-template-columns: 1fr 1fr;
  margin: 0;
  overflow: hidden;
  background-color: #fff;
}
.custom-cover {
  flex: 1;
  flex-direction: row;
  position: relative;
}
.card {
  padding: 0;
}
image {
  height: 20vh;
  width: 100%;
  border-radius: 5px;
}
.cover-content {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  height: 40px;
  background-color: rgba($color: #000000, $alpha: 0.4);
  display: flex;
  flex-direction: row;
  align-items: center;
  padding-left: 15px;
  font-size: 14px;
  color: #fff;
}
.popup-content {
  height: 80vh;
  background: white;
  position: relative;
  top: 5vh;
  padding: 20px 5px;

  .popup-content {
    padding: 20px;
    background-color: #f9f9f9;
    border-radius: 10px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  }
  .header {
    text-align: center;
    margin-bottom: 20px;
  }
  .title {
    font-size: 24px;
    font-weight: bold;
    color: #333;
  }
  .subtitle {
    font-size: 16px;
    color: #666;
  }
  .introduction {
    margin-bottom: 20px;
  }
  .intro-text {
    font-size: 14px;
    color: #333;
    line-height: 1.5;
  }
  .suggestions {
    margin-bottom: 20px;
  }
  .section-title {
    font-size: 18px;
    font-weight: bold;
    color: #333;
    margin-bottom: 15px;
  }
  .suggestion-item {
    margin-bottom: 15px;
  }
  .suggestion-title {
    font-size: 16px;
    margin-bottom: 5px;
    font-weight: bold;
    color: #333;
  }
  .suggestion-detail {
    font-size: 14px;
    color: #666;
    line-height: 1.5;
  }
  .additional-info {
    margin-bottom: 20px;
  }
  .info-text {
    font-size: 14px;
    color: #333;
    line-height: 1.5;
  }
}
</style>
