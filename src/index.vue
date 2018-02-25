<template>
  <div class="wrp" @viewappear="onShow" @viewdisappear="onHide">
    <navbar title="待办清单" :show-back="false"></navbar>
    <text v-if="todoEvents.length > 0" class="title">待办事件</text>
    <div class="evnets-wrp">
      <event-item 
        v-for="(event, index) in todoEvents"
        :key="event.name" :event="event" :index="index" 
        @click.native="onEventClick(event)" @onClickFinishButton="onFinish"
      ></event-item>
    </div>
    <text v-if="doneEvents.length > 0" class="title">已办事件</text>
    <div class="evnets-wrp">
      <event-item 
        v-for="(event, index) in doneEvents"
        :key="event.name" :event="event" :index="index"
        :showFinishButton="false"
        @click.native="onEventClick(event)"
      ></event-item>
    </div>
    <tab-bar @onAdd="onAdd" @onClear="onClear"></tab-bar>
  </div>
</template>

<script>
import navbar from './component/navbar.vue'
import tabbar from './component/tabbar.vue'
import eventItem from './component/event-item.vue'
import { getEntryUrl } from './utils'
const storage = weex.requireModule('storage')
const navigator = weex.requireModule('navigator')

export default {
  components: { navbar, tabBar: tabbar, eventItem },
  data () {
    return {
      todoEvents: [],
      doneEvents: []
    }
  },
  created () {
    if (weex.config.env.platform === 'Web') {
      this.onShow()
    }
  },
  methods: {
    onFinish (event, index) {
      this.todoEvents.splice(index, 1)
      this.doneEvents.push(event)
    },
    onAdd () {
      if (weex.config.env.platform === 'Web') {
        this.onHide()
      }
      navigator.push({
        url: getEntryUrl('add'),
        animated: 'true'
      })
    },
    onEventClick (event) {
      if (weex.config.env.platform === 'Web') {
        this.onHide()
      }
      storage.setItem('curEvent', JSON.stringify(event))
      navigator.push({
        url: getEntryUrl('detail'),
        animated: 'true'
      })
    },
    onClear () {
      this.todoEvents = []
      this.doneEvents = []
    },
    onHide () {
      storage.setItem('todoEvents', JSON.stringify(this.todoEvents))
      storage.setItem('doneEvents', JSON.stringify(this.doneEvents))
    },
    onShow () {
      storage.getItem('todoEvents', (e) => {
        if (e.result === 'success') {
          this.todoEvents = JSON.parse(e.data)
        } else {
          this.todoEvents = []
        }
      })
      storage.getItem('doneEvents', (e) => {
        if (e.result === 'success') {
          this.doneEvents = JSON.parse(e.data)
        } else {
          this.doneEvents = []
        }
      })
    }
  }
}
</script>

<style scoped>
.wrp {
  background-color: #f0efe9;
}
.title {
  font-size: 24px;
  padding-top: 20px;
  padding-bottom: 10px;
  padding-left: 20px;
  padding-right: 20px;
  color: #3e434f;
}
</style>
