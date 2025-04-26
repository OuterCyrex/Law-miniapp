<template>
  <view class="container">
    <view class="message-container">
      <scroll-view :scroll-y="true" v-for="(m, i) in history.messages" :key="i">
        <view class="message-row">
          <view class="ai-avatar">
            <image src="/static/ai-avatar.png" class="ai-avatar-img"/>
          </view>
          <view class="ai-avatar-text">
            <text>{{m.content}}</text>
          </view>
        </view>
      </scroll-view>
    </view>
    <view class="input-bar">
      <image class="new-session-button" src="/static/new-session.png" />
      <uni-easyinput></uni-easyinput>
    </view>
  </view>
</template>

<script lang="ts">
  import { ref } from 'vue'
  import { DefaultMessage } from "@/pages/ai/messages";

  class Message {
    role: 'ai' | 'user' = 'ai'
    content: string = ''
    constructor(role: 'ai' | 'user' = 'ai', content: string = '') {
      this.content = content
      this.role = role
    }
  }

  class History {
    messages: Array<Message> = []
    length: number = 0
    constructor() {
      this.messages = new Array<Message>()
    }
    public push(message: Message): void {
      this.messages.push(message)
    }
  }

  const AI = 'ai' as const;
  const User = 'user' as const;

  export default {
    setup() {
      let history = ref<History>(new History())
      history.value.push(new Message(AI, DefaultMessage.Introduction))
      history.value.push(new Message(AI, DefaultMessage.Greet))

      return {
        history
      }
    }
  }
</script>


<style scoped lang="scss">
.divider {
  width: 100%;
  height: 1px;
  background-color: #ccc;
  margin: 6px 0;
}
  .container {
    margin-top: 20px;
  }
  .message-container {
    height: 100%;
  }
  .input-bar {
    display: flex;
    margin: 16px 8px;
    position: fixed;
    top: calc(100vh - 60px);
  }
  .message-row {
    margin: 6px 12px;
    display: flex;
  }
  .ai-avatar-img {
    border-radius: 50%;
    height: 60rpx;
    width: 60rpx;
    margin-right: 10px;
  }
  .ai-avatar-text {
    background-color: #dfdfdf;
    padding: 8px;
    border-radius: 0 5px 5px 5px;
  }
  .new-session-button {
    height: 30px;
    width: 30px;
    margin: 4px;
  }
</style>
