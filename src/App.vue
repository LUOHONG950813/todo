<template>
  <div class="todoapp">
    <TodoHeader @btn="handleAdd" :arr="list"></TodoHeader>
    <TodoMain :arr="showArr"></TodoMain>
    <TodoFooter @clear="handleClear" :arr="list" @changeType="handleChangeType"></TodoFooter>
  </div>
</template>

<script>
import './styles/base.css'
import './styles/index.css'
import TodoHeader from './components/TodoHeader.vue'
import TodoMain from './components/TodoMain.vue'
import TodoFooter from './components/TodoFooter.vue'
export default {
  data() {
    return {
      // list: [
      //   { id: 100, name: '吃饭', isDone: true },
      //   { id: 201, name: '睡觉', isDone: false },
      //   { id: 103, name: '打豆豆', isDone: true },
      // ],
      list: JSON.parse(localStorage.getItem('todoList')) || [],
      type: 'all',
    }
  },
  watch: {
    list: {
      deep: true,
      handler() {
        localStorage.setItem('todoList', JSON.stringify(this.list))
      },
    },
  },
  components: {
    TodoHeader,
    TodoMain,
    TodoFooter,
  },
  methods: {
    handleAdd(tName) {
      let id = 100
      if (this.list.length > 0) {
        id = this.list[this.list.length - 1].id + 1
      }
      this.list.push({
        id: id,
        name: tName,
        isDone: false,
      })
    },
    handleClear() {
      this.list = this.list.filter(item => item.isDone === false)
    },
    handleChangeType(type) {
      this.type = type
    },
  },
  computed: {
    showArr() {
      if (this.type === 'yes') {
        return this.list.filter(item => item.isDone === true)
      } else if (this.type === 'no') {
        return this.list.filter(item => item.isDone === false)
      } else {
        return this.list
      }
    },
  },
}
</script>

<style></style>
