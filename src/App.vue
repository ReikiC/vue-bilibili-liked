<template>
  <div>
    <hi> hi {{ msg }} </hi>
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
      todos: [
        { title: 'eat', done: true },
        { title: 'sleep', done: false },
        { title: 'code', done: true },
      ],
    }
  },
  computed: {
    doneCount() {
      return this.todos.filter((v) => v.done).length
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
