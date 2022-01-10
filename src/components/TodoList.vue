<template>
  <form @submit.prevent="submit" class="form">
    <label>Name</label>
    <input v-model="formModel.name" />

    <button @click="addTodo" type="button">Add</button>
  </form>

  <div v-for="(todo, i) of todos" :key="i" class="todo">
    {{ todo.name }}
    <button @click="removeTodo(i)">Remove</button>
  </div>
</template>

<script>
  import { ref } from 'vue';

  export default {
  components: {  },
    name: 'TodoList',
    props: {
      name: {
        type: String,
        required: false,
        default: ''
      },
    },
    setup(_, { emit }) {
      const formModel = ref({
        name: '',
        category: ''
      })

      const todos = ref([])

      const addTodo = () => {
        todos.value.push({
          id: Math.random(),
          name: formModel.value.name,
          created: new Date()
        })
        emit('newTodo')
      }

      const removeTodo = (index) => {
        todos.value.splice(index, 1)
        emit('removeTodo')
      }

      const submit = () => {
        console.log('submitted')
      }

      return {
        formModel,
        todos,
        addTodo,
        removeTodo,
        submit
      }
    },
    emits: ['newTodo', 'removeTodo']
  }
</script>

<style>
.form {
  margin-bottom: 1rem; 
}

.todo {
  border: 1px solid red;
  margin-bottom: 1rem;
}
</style>