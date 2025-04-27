<template>
  <view class="container">
    <view class="cards-container">
      <uni-card class="card" padding="0" spacing="0" margin="10px" shadow="0px 0px 3px 1px rgba(0, 0, 0, 0.08)" v-for="(c, i) in parts" :key="i">
        <template v-slot:cover>
          <view class="custom-cover">
            <image class="cover-image" mode="aspectFill" :src="c.img">
            </image>
            <view class="cover-content">
              <text class="uni-subtitle uni-white">{{ c.title }}</text>
            </view>
          </view>
          <uni-list :border="false">
            <uni-list-item title="点击在线咨询" showArrow></uni-list-item>
          </uni-list>
        </template>
      </uni-card>
    </view>
  </view>
</template>

<script lang="ts">
import { ref } from 'vue'

class AdvicePart {
  img: string = ''
  title: string = ''

  constructor(title: string, img: string='') {
    this.img = img
    this.title = title
  }
}

export default {
  setup() {
    let parts = ref<Array<AdvicePart>>(
        [
            new AdvicePart('校园安全', '/static/adviceCover/school-security.jpeg'),
            new AdvicePart('网络保护', '/static/adviceCover/network-security.jpeg'),
            new AdvicePart('家庭权益', '/static/adviceCover/family-right.jpeg'),
            new AdvicePart('财务丢失', '/static/adviceCover/lost-found.png'),
            new AdvicePart('校园欺凌', '/static/adviceCover/school-bully.png'),
        ]
    )

    return {
      parts,
    }
  }
}

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
</style>
