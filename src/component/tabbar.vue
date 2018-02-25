<template>
  <div class="tabbar-wrp">
    <div class="tabbar-item" @click="onAdd">
      <text class="iconfont tabbar-icon">&#xe8a6;</text>
      <text class="tabbar-text">添加</text>
    </div>
    <div class="tabbar-item" @click="onClear">
      <text class="iconfont tabbar-icon">&#xe8c1;</text>
      <text class="tabbar-text">清空</text>
    </div>
  </div>
</template>

<script>
export default {
  name: 'tabbar',
  beforeCreate () {
    const domModule = weex.requireModule('dom')
    domModule.addRule('fontFace', {
      'fontFamily': "iconfont",
      'src': "url('http://at.alicdn.com/t/font_571013_3jfs8b3sidxwdn29.ttf')"
    })
  },
  methods: {
    onAdd () {
      this.$emit('onAdd')
    },
    onClear () {
      this.$emit('onClear')
    }
  }
}
</script>

<style scoped>
.iconfont {
  font-family: iconfont;
  color: #3e434f;
}
.tabbar-wrp {
  position: absolute;
  bottom: 0;
  left: 0;
  width: 750px;
  height: 88px;
  background-color: #FFF;
  flex-direction: row;
  align-items: center;
  border-top-width: 2px;
  border-color: #e2e2e2;
}
.tabbar-item {
  flex: 1;
  text-align: center;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.tabbar-text {
  font-size: 24px;
  color: #3e434f;
}
.tabbar-icon {
  font-size: 44px;
}
</style>


