<template>
  <view class="container">
    <view class="message-container">
      <scroll-view :scroll-y="true" v-for="(m, i) in history.messages" :key="i">
        <view class="message-row">
          <view v-if="m.role === 'ai'" class="ai-avatar">
            <image src="https://outer-pictures.oss-cn-beijing.aliyuncs.com/ai-avatar.png" class="ai-avatar-img"/>
          </view>
          <view v-if="m.role === 'ai'" class="ai-avatar-text">
            <text>{{m.content}}</text>
          </view>
          <view v-if="m.role === 'user'" class="user-avatar-text">
            <text>{{m.content}}</text>
          </view>
        </view>
      </scroll-view>
    </view>
    <view class="input-bar">
      <image class="new-session-button" @click="newSession" src="/static/new-session.png" />
      <uni-easyinput v-model="userInput" class="input-area"></uni-easyinput>
      <view class="send-button" @click="sendMessage">
        <text>发送</text>
      </view>
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

    public clear(): void {
      this.messages = []
      this.length = 0
    }
  }

  const AI = 'ai' as const
  const User = 'user' as const

  export default {
    setup() {
      let history = ref<History>(new History())
      history.value.push(new Message(AI, DefaultMessage.Introduction))

      let userInput = ref<string>('')

      const sendMessage = () => {
        history.value.push(new Message(User, userInput.value))
        userInput.value = ''
        setTimeout(() => {
          history.value.push(new Message(AI, DefaultMessage.Response))
        }, 2000)
      }

      const newSession = () => {
        history.value.clear()
        setTimeout(() => {
          history.value.push(new Message(AI, DefaultMessage.Introduction))
        }, 1000)
      }
      return {
        history,
        sendMessage,
        userInput,
        newSession,
      }
    }
  }
</script>


<style scoped lang="scss">
  .container {
    margin-top: 20px;
  }
  .message-container {
    padding-bottom: 80px;
  }
  .input-bar {
    background-color: #f6f6f6;
    padding: 2vw;
    display: flex;
    margin: 0;
    position: fixed;
    top: calc(100vh - 52px);
    justify-content: space-between;
    width: 96vw;
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
  .user-avatar-text {
    margin-left: auto;
    justify-items: flex-end;
    border-radius: 5px 0 5px 5px;
    background-color: #dfdfdf;
    padding: 8px;
  }
  .new-session-button {
    height: 30px;
    width: 30px;
    margin: 4px 8px;
  }
  .send-button {
    border-radius: 10px;
    background-color: #007aff;
    color: white;
    width: 60px;
    margin-left: 10px;
    display: flex;
    justify-content: center;
    align-items: center;
  }
</style>
