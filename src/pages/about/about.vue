<template>
	<view>
		{{ a }}
	</view>
  <uni-card title="基础卡片" extra="额外信息">
    <text>这是一个基础卡片示例，此示例展示了一个标题加标题额外信息的标准卡片。</text>
  </uni-card>

</template>

<script lang="ts">
import { ref } from 'vue'

export default {
  setup() {
    const a = ref<number>(1)

    return {
      a
    }
  }
}
</script>

<style>

</style>
