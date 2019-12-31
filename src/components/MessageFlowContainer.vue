<!--
* 说明文档

* 传入参数
contactName: 联系人昵称 // type: String，必需
message: 信息 // type: [Object, Object, ...]，非必需。其中 Object 格式如下:
  [
    {
      msgRole: number, // 0 是自己，1 是对方
      id: 1, // 消息 id
      type: 1, // 消息类型：1: 文本，2: 图片，3: 视频，4:音频，5: 系统信息，其他类型展示为 “暂未支持的消息类型”
      content: '你好', // 内容，当 type 为 1 和其他类型时是文本消息，当 2，3，4，5 时是链接地址
      time: new Date().toLocaleString() // 当前消息时间
    },
    ...
  ]
myAvatar: 我的头像地址 // type: String，必需
contactAvatar: 联系人头像地址 // type: String，必需
-->

<template>
  <div class="container">
    <div
      id="wx-view-container"
      class="wx"
    >
      <!-- 无数据时 -->
      <div
        v-if="message && message.length === 0"
        class="loading"
      >
        <div class="no-more">
          <span>暂无聊天记录</span>
        </div>
      </div>
      <!-- 有数据时 -->
      <div
        v-if="message && message.length > 0"
        class="title"
      >
        <p class="pull-left"> &lt; 返回 </p>
        <p>{{ contactName }}</p>
      </div>
      <MessageFlow
        v-if="message && message.length > 0"
        @scrollLoad="loadMessage"
      >
        <div class="msg">
          <ul>
            <li
              v-for="(msg, index) in message"
              :key="index"
            >
              <div class="time">
                <span>{{ msg.time }}</span>
              </div>
              <div :class="'main' + (msg.msgRole === 0?' self':'')">
                <img
                  :src="msg.msgRole === 0 ? myAvatar: contactAvatar"
                  class="avatar"
                >
                <!-- 文本/和系统信息 -->
                <div
                  v-if="msg.type === 1 || msg.type === 5"
                  :class="[msg.type === 5 ? 'system': 'text']"
                >
                  <span>{{ msg.content }}</span>
                </div>
                <!-- 图片 -->
                <div
                  v-else-if="msg.type === 2"
                  class="text"
                >
                  <img
                    :src="msg.content"
                    class="image"
                    alt="聊天图片"
                  >
                </div>
                <!-- 视频 -->
                <div
                  v-else-if="msg.type === 3"
                  class="text"
                >
                  <video
                    :src="msg.content"
                    controls="controls"
                    style="width: 100%;height: 100%;"
                  />
                </div>
                <!-- 音屏 -->
                <div
                  v-else-if="msg.type === 4"
                  class="text"
                >
                  <audio
                    :src="msg.content"
                    controls="controls"
                    style="height: 30px;width: 180px;"
                  />
                </div>
                <!-- 其他 -->
                <div
                  v-else
                  class="text"
                >
                  [暂未支持的消息类型: {{ msg.content }}]
                </div>
              </div>
            </li>
          </ul>
        </div>
      </MessageFlow>
    </div>
  </div>
</template>

<script>
import MessageFlow from './MessageFlow.vue'

export default {
  name: 'MessageFlowContainer',
  components: {
    MessageFlow
  },
  props: {
    contactName: {
      type: String,
      required: true,
      default: 'Bevis'
    },
    message: {
      type: Array,
      required: false,
      default() {}
    },
    myAvatar: {
      type: String,
      required: true,
      default: ''
    },
    contactAvatar: {
      type: String,
      required: true,
      default: ''
    }
  },
  data() {
    return {
      isUpperLaoding: false
    }
  },
  methods: {
    loadMessage(done) {
      if (!this.isUpperLaoding) {
        this.isUpperLaoding = true
        setTimeout(() => {
          let id = this.mockRandom(1, 10)
          let role = this.mockRandom(0, 2)
          let data = this.mockData(id, role) // 这里可以修改为 ajax，那 url 可以作为参数传入做配置
          this.message.unshift(data)
          this.isUpperLaoding = false
          done(true)
        }, 500)
      }
    },
    // 生成 n-m 之间的随机数字
    mockRandom(n, m) {
      return Math.floor(Math.random() * (n - m) + m)
    },
    mockData(id, role, count) {
      return {
        msgRole: role,
        type: 1,
        content: 'hello???',
        time: new Date().toLocaleString(),
        id: id
      }
    }
  }
}
</script>

<style scoped lang="less">
  @import url('../styles/MessageFlowContainer.less');
</style>
