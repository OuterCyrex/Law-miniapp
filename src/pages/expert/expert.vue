<template>
  <view class="container">
    <view class="search-bar">
      <uni-search-bar
          @input="searchExpert"
          @cancel="searchExpert('')"
          radius="15px"
          @clear="searchExpert('')"
          clear-button="always"
          cancelButton="always"
          placeholder="搜索咨询师"
      ></uni-search-bar>
    </view>
  <view>
    <view class="scroll-content" >
      <view v-for="(e, i) in filterExperts" :key="i" class="experts">
        <uni-card
            :is-shadow="true"
            padding="5px"
            radius="15px"
        >
          <uni-row>
            <uni-col :span="6">
              <view style="margin: 5px 15px 5px 0; height: 12vh;">
                <image
                    style="width: 100%; height: 100%; object-fit: contain; border-radius: 5px;"
                    :src="e.avatar"
                ></image>
              </view>
            </uni-col>
            <uni-col :span="18">
              <view class="card-title">
                <uni-title type="h2" :title="e.name"></uni-title>
                <view class="ask-button">
                  <uni-tag text="点击咨询" type="warning" />
                </view>
              </view>
              <uni-icons type="forward"></uni-icons>
              <text style="line-height:24px;"> {{e.address}}</text>
              <view class="divider"></view>
              <view>
                <uni-icons type="chat-filled"></uni-icons>
                <text style="margin: 0 8px 0 4px; font-size: 12px; color: #4cd964;">在线</text>
                <uni-icons type="phone-filled"></uni-icons>
                <text style="margin: 0 2px; font: 13px bold">{{e.phone }}</text>
              </view>
            </uni-col>
          </uni-row>
        </uni-card>
      </view>
        </view>
  </view>
      <uni-load-more/>
    </view>
</template>

<script lang="ts">
  import { ref } from "vue";

  class ExpertInfo {
    name: string = ''
    address: string = ''
    avatar: string = ''
    phone: string = '15660889001'

    constructor(name: string, address: string, phone?: string) {
      this.name = name
      this.address = address
      this.avatar = '/static/lawyer-avatar.jpg'
      this.phone = phone || '15660889001'
    }
  }

  interface swiperImg {
    src: string
  }

  export default {
    setup() {
      const experts: Array<ExpertInfo> = [
          new ExpertInfo('杨燕', '四川蓉桦律师事务所', '15835510921'),
          new ExpertInfo('陆芮竺', '四川致高律师事务所', '19660021256'),
          new ExpertInfo('卞德志', '北京大成（成都）律师事务所', '13887711092'),
          new ExpertInfo('杜孟繁', '四川佰霖律师事务所', '159717666112'),
      ]

      let filterExperts = ref<Array<ExpertInfo>>(experts)

      const searchExpert: (input: string) => void = (input: string) => {
        if (input === '') {
          filterExperts.value = experts
        } else {
          filterExperts.value = experts.filter(
              e => e.name.includes(input) || e.address.includes(input),
          )
        }
      }

      return {
        filterExperts,
        searchExpert,
      }
    }
  }
</script>


<style scoped lang="scss">
.container {
  height: 100vh;
}
.divider {
  width: 100%;
  height: 1px;
  background-color: #ccc;
  margin: 6px 0;
}
text {
  position: relative;
  bottom: 1.5px;
}
.card-title {
  display: flex;
  align-items: center;
  justify-content: flex-start;
}
.ask-button {
  margin-left: auto;
}
.search-bar {
  background-color: #e8e8e8;
  z-index: 10;
}
.scroll-content {
  z-index: -1;
}
</style>
