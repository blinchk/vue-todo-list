<template>
  <div>
    <ul>
      <TodoItem
          v-for="(todo, i) of todos"
          v-bind:index="i"
          v-bind:todo="todo" :key="todo.id"
          v-on:remove-todo="removeTodo"
      />
    </ul>
  </div>
</template>

<script>
import TodoItem from "@/components/TodoItem"
export default {
  name: "TodoList",
  props: ['todos'],
  components: {
    TodoItem
  },
  methods: {
    removeTodo(id) {
      this.$emit('remove-todo', id)
    }
  }
}
</script>

<style scoped>

</style>