<template>
  <div id="app">
    <AddTodo v-on:add-todo="addTodo"/>
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo"/> 
    <!-- // v-bind is passing in todos array from the data function below -->
    
  </div>
</template>

<script>


import Todos from '../components/Todos'
import AddTodo from '../components/AddTodo'
import axios from 'axios'

export default {
  name: 'Home',
  components: {
    Todos,
    AddTodo
  },

  data() {
    return {
      todos: []
    }
  },
  methods: {

    deleteTodo(id) {
      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
      .then(() => this.todos = this.todos.filter(todo => todo.id !== id))
      .catch(err => console.log(err))
      
    },

    addTodo(newTodo) {
      const { title, completed } = newTodo
      // mimicing a backend API
      axios.post('https://jsonplaceholder.typicode.com/todos', {
        title,
        completed
      })
      .then(res => this.todos = [...this.todos, res.data])
      .catch(err => console.log(err)) 
    }

  },
  // get todo data frome external API and set the limit of how many are displayed to 5
  created() {
    axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5') 
      .then(res => this.todos = res.data)
      .catch(err => console.log(err))

  }

}
</script>

<style>

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body { 
  font-family: Arial, Arial, Helvetica, sans-serif;
  line-height: 1.4;
}

.btn {
  display: inline-block;
  border: none;
  background: #555;
  color: #fff;
  padding: 7px 20px;
  cursor: pointer;
}

</style>

