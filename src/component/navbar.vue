<template>
  <div class="navbar">
    <text v-if="showBack" class="iconfont navbar-icon" @click="onBack">&#xe8b5;</text>
    <text v-else class="navbar-title"></text>
    <text class="navbar-title">{{title}}</text>
    <text class="navbar-title"></text>
  </div>
</template>

<script>
const navigator = weex.requireModule('navigator')

export default {
  name: 'navbar',
  props: {
    showBack: {
      type: Boolean,
      default: true
    },
    title: {
      type: String,
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
    onBack () {
      navigator.pop({
        animated: 'true'
      })
    }
  }
}
</script>

<style scoped>
.iconfont {
  font-family: iconfont;
}
.navbar {
  height: 88px;
  background-color: #50e3a4;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  padding-left: 20px;
  padding-right: 20px;
}
.navbar-title {
  color: #FFFFFF;
  font-size: 32px;
}
.navbar-icon {
  color: #FFFFFF;
  font-size: 36px;
}
</style>

