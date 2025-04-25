<template>
	<view>
		{{ a }}
	</view>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue'

export default defineComponent({
  setup() {
    const a = ref<number>(1)

    return {
      a
    }
  }
})
</script>

<style>

</style>
