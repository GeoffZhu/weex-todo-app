<template>
  <div class="event">
    <text class="label">{{event.name}}</text>
    <div class="evnet-btn-wrp">
      <text v-if="showFinishButton" class="btn" @click="onFinish(event, index)">完成</text>
      <text class="iconfont">&#xe88e;</text>
    </div>
  </div>
</template>

<script>
export default {
  name: 'event-item',
  props: {
    showFinishButton: {
      type: Boolean,
      default: true
    },
    index: {
      type: Number,
      required: true
    },
    event: {
      type: Object,
      required: true
    }
  },
  beforeCreate () {
    const domModule = weex.requireModule('dom')
    domModule.addRule('fontFace', {
      'fontFamily': "iconfont",
      'src': "url('http://at.alicdn.com/t/font_571013_3jfs8b3sidxwdn29.ttf')"
    })
  },
  methods: {
    onFinish (event, index) {
      this.$emit('onClickFinishButton', event, index)
    }
  }
}
</script>

<style scoped>
.iconfont {
  font-family: iconfont;
  color: #3e434f;
}
.event {
  background-color: #FFF;
  flex-direction: row;
  align-items: center;
  justify-content: space-between;
  padding-left: 20px;
  padding-right: 20px;
  height: 80px
}
.label {
  color: #3e434f;
  font-size: 28px;
}
.evnet-btn-wrp {
  flex-direction: row;
  align-items: center;
}
.btn {
  border-radius: 10px;
  font-size: 24px;
  padding-left: 18px;
  padding-right: 18px;
  padding-top: 2px;
  padding-bottom: 2px;
  background-color: #50e3a4;
  color: #ffffff;
}
</style>


