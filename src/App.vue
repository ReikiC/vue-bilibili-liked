<template>
  <div>
    <h1>hi {{ msg }}</h1>
    <!-- <div @click="add">{{ count }}</div> -->

    <input type="text" v-model="val" @keypress.enter="addTodo" />
    <button @click="addTodo">add</button>
    <ul>
      <li v-for="todo in todos" :key="todo.title">
        <input type="checkbox" v-model="todo.done" />
        <span>
          {{ todo.title }}
        </span>
      </li>
    </ul>
    <div>
      <div><input type="checkbox" v-model="allDone" /> selectAll</div>
      {{ doneCount }} /
      {{ todos.length }}
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
export default defineComponent({
  data() {
    return {
      msg: 'Wellcome to Your Vue.js App',
      count: 1,
      val: '',
      todos: localStorage.getItem('todos')
        ? JSON.parse(localStorage.getItem('todos') as string)
        : [
            { title: 'eat', done: true },
            { title: 'sleep', done: false },
            { title: 'code', done: true },
          ],
    }
  },
  watch: {
    todos: {
      handler() {
        localStorage.setItem('todos', JSON.stringify(this.todos))
      },
      deep: true,
      immediate: true,
    },
  },
  computed: {
    allDone: {
      get() {
        return this.doneCount === this.todos.length
      },
      set(value: boolean) {
        this.todos.forEach((todo: { title: string; done: boolean }) => {
          todo.done = value
        })
      },
    },
    doneCount() {
      return this.todos.filter((v: { title: string; done: boolean }) => v.done).length
    },
  },
  methods: {
    add() {
      this.count++
    },
    addTodo() {
      this.todos.push({
        title: this.val,
        done: false,
      })
      this.val = ''
    },
  },
})
</script>

<style></style>
