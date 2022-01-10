<template>
  <h2>Todos</h2>
  <div class="todos">
    <TodoList @newTodo="onNewTodo" @removeTodo="onRemoveTodo" />
  </div>

  <h2>Stats</h2>
  <div class="stats">
    {{ counter }}
  </div>
</template>

<script>
import { ref } from 'vue'
import TodoList from './components/TodoList.vue'

export default {
  name: 'App',
  components: {
    TodoList
  },
  setup() {
    const counter = ref(0)

    const onNewTodo = () => {
      counter.value += 1
    }

    const onRemoveTodo = () => {
      counter.value -= 1
    }

    return {
      counter,
      onNewTodo,
      onRemoveTodo
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.todos {
  margin: 0 auto;
  width: 50%;
}
</style>
