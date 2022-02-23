<template>
  <footer class="footer">
    <span class="todo-count"
      >剩余<strong>{{ count }}</strong></span
    >
    <ul class="filters">
      <li>
        <a :class="{ selected: type === 'all' }" href="javascript:;" @click="change('all')">全部</a>
      </li>
      <li>
        <a :class="{ selected: type === 'no' }" href="javascript:;" @click="change('no')">未完成</a>
      </li>
      <li>
        <a :class="{ selected: type === 'yes' }" href="javascript:;" @click="change('yes')">已完成</a>
      </li>
    </ul>
    <button class="clear-completed" @click="clearAll">清除已完成</button>
  </footer>
</template>

<script>
export default {
  data() {
    return {
      type: 'all',
    }
  },
  props: ['arr'],
  methods: {
    clearAll() {
      this.$emit('clear')
    },
    change(type) {
      this.type = type
      this.$emit('changeType', this.type)
    },
  },
  computed: {
    count() {
      var newArr = this.arr.filter(item => item.isDone === false)
      return newArr.length
    },
  },
}
</script>
