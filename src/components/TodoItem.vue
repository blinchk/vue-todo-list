<template>
  <div>
    <li>
      <span v-bind:class="{done: todo.completed}">
        <input type="checkbox" v-on:change="todo.completed = !todo.completed">
        <strong>{{index+1}}</strong>
        {{todo.title | uppercase }}
      </span>
      <button class="rm" v-on:click="$emit('remove-todo', todo.id)">&times;</button>
    </li>
  </div>

</template>

<script>
export default {
  props: {
    todo: {
      type: Object,
      required: true
    },
    index: Number
  },
  filters: {
    uppercase(value) {
      return value
    }
  },
  name: "TodoItem"
}
</script>

<style scoped>
  li {
    border: 1px solid #ccc;
    display: flex;
    justify-content: space-between;
    padding: .5rem 2rem;
    margin-bottom: 1rem;
  }

  .rm {
    border-radius: 20%;
    background: tomato;
    border: 0;
    color: white;
    font-weight: bold;
  }

  .done {
    text-decoration: line-through;
  }
</style>