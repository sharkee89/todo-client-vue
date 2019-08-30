<template>
  <div id="app">
    <Header />
    <AddTodo v-on:add-todo="addTodo"/>
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo"/>
  </div>
</template>

<script>
import Header from './components/layout/Header';
import Todos from './components/Todos';
import AddTodo from './components/AddTodo';
import axios from 'axios';

export default {
  name: 'app',
  components: {
    Header,
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
      axios.delete(`https://young-dawn-58008.herokuapp.com/todos/${id}`)
        .then(this.todos = this.todos.filter((todo) => id !== todo['_id']))
        .catch(err => console.log(err));
    },
    addTodo(newTodo) {
      const { title, description, date } = newTodo;
      axios.post('https://young-dawn-58008.herokuapp.com/todos', {
        title,
        description,
        date
      })
        .then(res => {
          this.todos = [...this.todos, {
            title,
            description,
            date
          }]
        })
        .catch(err => console.log(err));
    }
  },
  created() {
    axios.get('https://young-dawn-58008.herokuapp.com/todos')
      .then(res => this.todos = res.data)
      .catch(err => console.log(err));
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
    font-family: Arial, Helvetica, sans-serif;
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
  .btn:hover {
    background: #666;
  }
</style>
