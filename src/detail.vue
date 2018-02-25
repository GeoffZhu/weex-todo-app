<template>
  <div class="wrp">
    <navbar title="详情"></navbar>
    <div class="form-item">
      <text class="title-text">{{name}}</text>
    </div>
    <div class="form-item">
      <text class="text">{{desc}}</text>
    </div>
  </div>
</template>

<script>
import navbar from './component/navbar.vue'
const storage = weex.requireModule('storage')
const navigator = weex.requireModule('navigator')
export default {
  name: 'detail',
  components: { navbar },
  data () {
    return {
      name: '',
      desc: ''
    }
  },
  created () {
    storage.getItem('curEvent', (e) => {
      if (e.result === 'success') {
        let event = JSON.parse(e.data)
        this.name = event.name
        this.desc = event.desc
      }
    })
  }
}
</script>

<style scoped>
.wrp {
  flex-direction: column;
  background-color: #f0efe9;
}
.form-item {
  flex-direction: row;
  padding-left: 30px;
  padding-right: 30px;
  margin-top: 30px;
}
.title-text {
  width: 690px;
  font-size: 28px;
  color: #3e434f;
}
.text {
  font-size: 26px;
  color: #3e434f;
}
</style>


