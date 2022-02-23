<template>
  <header class="header">
    <h1>todos</h1>
    <input id="toggle-all" class="toggle-all" type="checkbox" v-model="isAll" />
    <label for="toggle-all"></label>
    <input class="new-todo" placeholder="输入任务名称-回车确认" autofocus v-model="taskName" @keydown.enter="addTask" />
  </header>
</template>

<script>
export default {
  props: ['arr'],
  data() {
    return {
      taskName: '',
    }
  },
  methods: {
    addTask() {
      this.$emit('btn', this.taskName)
      this.taskName = ''
    },
  },
  computed: {
    isAll: {
      get() {
        return this.arr.length !== 0 && this.arr.every(item => item.isDone === true)
      },
      set(val) {
        this.arr.forEach(item => (item.isDone = val))
      },
    },
  },
}
</script>
