<template>
  <div class="wrp">
    <navbar title="添加事件"></navbar>
    <div class="form-item">
      <input v-model="name" type="text" placeholder="请输入事件名称" class="input"/>
    </div>
    <div class="form-item">
      <textarea v-model="desc" type="text" placeholder="请输入事件内容" class="textarea"/>
    </div>
    <div class="b-btn-wrp">
      <text class="b-btn" @click="onAdd">完成</text>
    </div>
  </div>
</template>

<script>
import navbar from './component/navbar.vue'
const storage = weex.requireModule('storage')
const navigator = weex.requireModule('navigator')

export default {
  name: 'add',
  components: { navbar },
  data () {
    return {
      name: '',
      desc: ''
    }
  },
  methods: {
    onAdd () {
      let todoEvents
      storage.getItem('todoEvents', (e) => {
        if (e.result === 'success') {
          todoEvents = JSON.parse(e.data)
        } else {
          todoEvents = []
        }
        todoEvents.push({
          name: this.name,
          desc: this.desc
        })
        storage.setItem('todoEvents', JSON.stringify(todoEvents), (e) => {
          if (e.result === 'success') {
            navigator.pop({
              animated: 'true'
            })
          }
        })
      })
    }
  }
}
</script>

<style scoped>
.iconfont {
  font-family: iconfont;
}
.wrp {
  flex-direction: column;
  background-color: #f0efe9;
}
.form-item {
  flex-direction: row;
  padding-left: 30px;
  padding-right: 30px;
  margin-top: 40px;
}
.input {
  flex: 1;
  font-size: 28px;
  background-color: transparent;
  color: #3e434f;
}
.textarea {
  flex: 1;
  font-size: 26px;
  background-color: transparent;
  color: #3e434f;
}
.b-btn-wrp {
  position: absolute;
  bottom: 60px;
  left: 75px;
  width: 600px;
  height: 80px;
  background-color: #50e3a4;
  flex-direction: row;
  align-items: center;
  border-radius: 12px;
}
.b-btn {
  flex: 1;
  text-align: center;
  font-size: 28px;
  color: #FFFFFF;
}
</style>


