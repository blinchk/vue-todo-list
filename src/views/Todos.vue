<template>
  <div>
    <h2>To-Do List</h2>
    <AddTodo @add-todo="addTodo"></AddTodo>
    <select v-model="filter">
      <option value="all">All</option>
      <option value="completed">Completed</option>
      <option value="not-completed">Not Completed</option>
    </select>
    <hr>
    <Loader v-if="loading"/>
    <TodoList v-else-if="filteredTodos.length"
              v-bind:todos="filteredTodos"
              @remove-todo="removeTodo"
    />
    <p v-else>No todos!</p>
  </div>
</template>

<script>
import TodoList from "@/components/TodoList"
import Loader from "@/components/Loader";
import AddTodo from "@/components/AddTodo"
export default {
  name: 'App',
  data() {
    return {
      todos: [],
      loading: true,
      filter: 'all'
    }
  },
  mounted() {
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=3') // загрузка JSON
        .then(response => response.json())
        .then(json => {
        this.todos = json
        this.loading = false
        })
  },
  components: { // подключенные компоненты
    TodoList,
    AddTodo,
    Loader
  },
  /* watch: { // отслеживание переменной
    filter(value) {
    }
  }, */
  computed: {
    filteredTodos() {
      if (this.filter === 'completed') {
        return this.todos.filter(t => t.completed)
      }
      else if (this.filter === 'not-completed') {
        return this.todos.filter(t => !t.completed)
      }
      else {
        return this.todos
      }
    }
  },
  methods: { // методы списка
    removeTodo(id) {
      this.todos = this.todos.filter(t => t.id !== id)
    },
    addTodo(todo) {
      this.todos.push(todo)
    }
  }
}
</script>