<template>
  <div id="app">
    <MessageFlowContainer
      :contact-name="contactName"
      :contact-avatar="contactAvatar"
      :my-avatar="myAvatar"
      :message="messageList"
    />
  </div>
</template>

<script>
import MessageFlowContainer from './components/MessageFlowContainer.vue'
import contactAvatarImg from './assets/contactAvatar.png'
import myAvatarImg from './assets/myAvatar.png'
import imgSrc from './assets/logo.png'
import videoSrc from './assets/cat.mp4'
import audioSrc from './assets/horse.mp3'

export default {
  name: 'App',
  components: {
    MessageFlowContainer
  },
  data() {
    return {
      contactName: 'Bevis',
      contactAvatar: contactAvatarImg,
      myAvatar: myAvatarImg,
      messageList: [
        {
          msgRole: 0,
          id: 1,
          type: 1,
          content: 'hello Bevis!',
          time: new Date().toLocaleString()
        },
        {
          msgRole: 1,
          id: 1,
          type: 1,
          content: 'hello world!',
          time: new Date().toLocaleString()
        },
        {
          msgRole: 1,
          id: 2,
          type: 2,
          content: imgSrc,
          time: new Date().toLocaleString()
        },
        {
          msgRole: 0,
          id: 3,
          type: 3,
          content: videoSrc,
          time: new Date().toLocaleString()
        },
        {
          msgRole: 0,
          id: 4,
          type: 4,
          content: audioSrc,
          time: new Date().toLocaleString()
        },
        {
          msgRole: 1,
          id: 5,
          type: 5,
          content: 'xxx添加xxx到群组里',
          time: new Date().toLocaleString()
        }, {
          msgRole: 0,
          id: 6,
          type: 6,
          content: '请打开小程序',
          time: new Date().toLocaleString()
        }
      ]
    }
  }
}
</script>

<style lang="less">
  * {
    margin: 0px;
    padding: 0px;
    font-family: Helvetica Neue, Helvetica, PingFang SC, Hiragino Sans GB, Microsoft YaHei, SimSun, sans-serif;
    font-size: 14px;
    -webkit-font-smoothing: antialiased;
  }

  #app {
    width: 100%;
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    color: #2c3e50;
    background-color: rgb(239, 239, 239);
  }
</style>
