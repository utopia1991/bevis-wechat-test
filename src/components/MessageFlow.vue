
<template>
  <div>
    <div
      ref="pullRefresh"
      class="msg-container"
      @touchstart="startTouch"
      @touchmove="touching"
      @touchend="endTouch"
    >
      <div class="loading-text">
        {{ loadText }}
      </div>
      <slot />
    </div>
  </div>
</template>

<script>
export default {
  name: 'MessageFlow',
  data() {
    return {
      targetEl: null,
      loadText: '',
      start: 0,
      height: 0
    }
  },
  mounted() {
    this.targetEl = this.$refs.pullRefresh
  },
  methods: {
    startTouch(e) {
      this.start = e.touches[0].pageY
    },
    touching(e) {
      this.height = e.touches[0].pageY - this.start
      if (this.height > 0 && this.height < 50) {
        this.loadText = '下拉获取数据'
        this.targetEl.style.transform = 'translateY(' + this.height + 'px)'
      }
    },
    endTouch(e) {
      this.targetEl.style.transform = 'translateY(0px)'
      this.loadText = '拉取数据中...'
      this.$emit('scrollLoad', (isFinish) => {
        if (isFinish) {
          this.loadText = ''
        }
      })
    }
  }
}
</script>

<style lang="less" scoped>
  @import url('../styles/MessageFlow.less');
</style>
