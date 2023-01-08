<template>
  <div id="app">
    <h1>Just do it.</h1>
    <CommonClock />
    <AddTodo
        @add-todo="addTodo"
    ></AddTodo>
    <TodoList
        v-if="todos.length"
        v-bind:todos="todos"
        v-on:toggle="onToggle"
        v-on:remove="onRemove"
    >
    </TodoList>
    <p v-else>No todos!</p>
  </div>
</template>

<script>
import TodoList from '@/components/TodoList'
import AddTodo from '@/components/AddTodo'
import CommonClock from "@/components/CommonClock";

export default {
  name: 'App',

  data() {
    return {
      todos: []
    }
  },

  components: {
    TodoList,
    AddTodo,
    CommonClock
  },

 created () {
    const list = localStorage.getItem('todo-list')
    if (list) {
      this.todos = JSON.parse(list)
    }
  },

  methods: {
    onToggle ({id, value}) {
      if (this.todos.find(todo => todo.id === id)) {
        this.todos.find(todo => todo.id === id).completed = value;
      } else {
        console.log('хуй')
      }
    },

    onRemove (id) {
      this.todos = this.todos.filter(todo => todo.id !== id).map(todo => {
        if (todo.id > id) {
          // todo.id = todo.id - 1
          return  {...todo, id: todo.id - 1}
        } else {
          return todo
        }
      })
    },

    addTodo (title) {
      this.todos.push({
        id: this.todos.length + 1,
        title,
        completed: false
      });
    }
  },

  watch: {
    todos: {
      deep: true,
      handler (newValue) {
        localStorage.setItem('todo-list', JSON.stringify(newValue))
      }
    },

    date: {
      deep: true,
      handler (newValue) {
        this.date = newValue
      }
    }
  }
}
</script>

<style>
  #app {
    font-family: 'Inter', sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
   body {
     background: rgb(25,58,135);
     background: linear-gradient(90deg, hsl(241, 1%, 33%) 0%, hsl(198, 75%, 14%) 100%) fixed;
   }

   h1 {
     color: hsl(8, 60%, 92%);
     font-size: 100px;
     font-weight: 300;
   }

   .date {
       color: hsl(8, 60%, 92%);
       margin-bottom: 7px;
   }
</style>
