<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <h1>To do App</h1>
    <router-link href="/todos">Todos</router-link>
    <hr>
    <AddTodo
        @add-todo="addTodo"
    />
    <hr>
    <TodoList
        v-bind:todos="todos"
        @remove-todo="removeTodo"
    />
  </div>
</template>


<script>
  import TodoList from "@/components/TodoList"
  import AddTodo from "@/components/AddTodo"
  export default {
    name: 'App',
    data() {
      return {
        todos: [
          {id: 1, title: 'Buy bread', completed: false},
          {id: 2, title: 'Buy batter', completed: false},
          {id: 3, title: 'Buy beer', completed: false},
        ]
      }
    },
    mounted() {
      fetch('https://jsonplaceholder.typicode.com/todos?_limit=3')
      .then(response => response.json())
      .then(json => this.todos = json)
    },
    methods: {
      removeTodo(id) {
        this.todos = this.todos.filter(t => t.id !== id)
      },
      addTodo(todo) {
        this.todos.push(todo)
      }
    },
    components: {
      TodoList,
      AddTodo
    }
  }
</script>